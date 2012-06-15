---
layout: post
title: Modern OpenGL
---

I've spent the last couple of weeks working on some code for The University of Leeds. Rather than actual research, this time has been spent on learning and adapting my code to be more compliant with OpenGL. I've done away with OpenFrameworks. It's now a mixture of [PCL](http://pointclouds.org/), [OpenCV](opencv.willowgarage.com), [Boost](http://www.boost.org/), [GLM](http://glm.g-truc.net/) and [QT](http://qt.nokia.com/products/). I'm not so happy about the last one but it works at least. I've effectively, almost recreated Cinder under Linux (well, kind of).

OpenGL 4.2 is a little different from the OpenGL I learnt at Manchester - quite so. Gone are calls to *glBegin* and similar. Everything is handled with buffers, shaders and Vertex Array Objects. In addition, geometry shaders become more important. All the calls to push and pop matrices are gone too. In addition, we need to control all our views manually; no more *gluLookAt* or similar. But where to begin?

Firstly, we need a way to create a context. A context is essentially a setup or agreement with the underlying windowing system. For example, we kmight want a window with double buffering, alpha blending, full-screen anti-aliasing. There are a few ways of doing this. I've found that [FreeGlut](http://freeglut.sourceforge.net/), [GLFW](http://www.glfw.org/) and [QT](http://qt.nokia.com/products/) are probably the best. The sad thing is, we are still relying on GLUT in libraries such as [OpenFrameworks](http://www.openframeworks.cc/). [Cinder](http://libcinder.org/) uses native extensions which is another good option. Under Linux however, things are trickier as the wxWidgets is quite old. OSX certainly has the prettiest native extensions but we can create quite nice things with the above. 

The problem with most of these libraries is the lack of a decent GUI. QT has been slammed for being old and bloaty. OpenFrameworks has some fairly good GUIs such as [ofxUI](https://github.com/rezaali/ofxUI). Cinder has the [AntTweakBar](http://www.antisphere.com/Wiki/tools:anttweakbar). Some of these have problems with OpenGL 3.3 and above though. There is a nice heavyweight, middleware library called [Rocket](http://librocket.com/) that looks interesting.

So what do we need to do to get a context and draw our triangles? Once we have the context, we need to load the extensions and map these to the libraries in the disk. If we dont do this, all our OpenGL fancy functions will map to NULL. So, we need a library that loads things for us. Fortunately we have [GLEW](http://glew.sourceforge.net/).

    glewExperimental = TRUE;
    GLenum err=glewInit();
    if(err!=GLEW_OK) {
        //Problem: glewInit failed
        cout << "GLEWInit failed" << endl;
    }

This bit of code is really handy and we can't do much without it. At this point we can start our update and drawing loops. Its worth remembering that OpenGL is not thread safe; it's a state machine and the state is tied into the execution thread so make sure all your OpenGL calls are on the same thread.

Now we have all our extensions, we need to create what is known as a [Vertex Buffer](http://en.wikipedia.org/wiki/Vertex_Buffer_Object) Object or VBO. This is a buffer that is created in main memory and then uploaded on to our graphics card. Our shaders are bound to the context and the buffer is sent through the shader and our triangles appear. A VBO looks a little like this:

    vbo = new GLuint[s];
    glGenBuffers(s,vbo);
    glBindBuffer(GL_ARRAY_BUFFER, mVID);
    glBufferData(GL_ARRAY_BUFFER,
        mVertices.size() * sizeof(GLfloat), 
        &mVertices[0], GL_DYNAMIC_DRAW);

So we create a certain number of buffers. We then bind the buffer and then provide it with some data. In this case, mVertices is a std::vector<float> .

Now, we can add other things here, such as indices, texture co-ordinates, normals, colours and many other things. We can bundle these all together in a saved state called a [Vertex Array Object](http://www.opengl.org/wiki/Vertex_Array_Object). This is a handy piece of syntax that essentially allows us to recall all the buffer settings. 

No, we have a triangle specified but we also need a shader. In fact we need at least 2 and maybe 3. We need a [Fragment Shader](http://en.wikipedia.org/wiki/Shader#Pixel_shaders), a [Vertex Shader](http://en.wikipedia.org/wiki/Shader#Vertex_shaders) and we can also add a [Geometry Shader](http://en.wikipedia.org/wiki/Shader#Geometry_shaders) as well should we wish. Creating a shader is an interesting topic and there are many cool effects we can do. As my graphics card supports OpenGL4.2, I can write a simple shader like this:

    #version 420 compatibility
    out vec4 vertex_position;
    out vec2 texCoord;
    
    layout (location = 0) in vec3 attribVertPosition; // 1 is the indicies
    layout (location = 2) in vec2 attribVertTexCoord;
    
    uniform mat4 mMVPMatrix;
    
    void main() {            
        vertex_position = mMVPMatrix *
            vec4(attribVertPosition,1.0);
        gl_Position = vertex_position;
        texCoord = attribVertTexCoord;
    } 


This is the vertex shader and is probably the more complicated section in this simple example, because it has a *layout* directive. This basically states that the first buffer to be bound contains positions. The second buffer to be bound isn't used and the third buffer to be bound contains the texture co-ordinates. These indexes reflect the order and position of the vertex buffer objects we bound before.

Our fragment shader comes next:

    #version 420 compatibility
    in vec4 vertex_position;
    in vec2 texCoord;
    uniform sampler2DRect mBaseTex;
    
    void main() {
	    gl_FragColor = texture(mBaseTex,texCoord);
    }

This simple example just outputs the texel colour for that fragment. Simple enough.

So, we have a triangle or similar on our screen. How now do we deal with transformations? Remember *glRotatef* and *glTranslatef* ? These functions are part of what is called *Immediate Mode Rendering* . This technique is now old, inefficient and only supported for legacy apps. The reason is largely due to hardware. Its much better to perform graphics processing on the GPU. Take the iPhone and OpenGLES2 for instances. We simply don't have immediate mode rendering anymore. 

We need a second library to work with our matrices and similar. I've used OpenCV in the past but it doesn't have the most intuitive interface sadly. Fortunately, there is an amazing library called [GLM](http://glm.g-truc.net/) which I HIGHLY recommend everyone use. It's a great piece of kit. It is a header only library (which I love) and has all the matrix functions you could wish for. For example, here is a simple camera, written in GLM

    mObj->mHoriz += static_cast<float_t>(dx) * (sSense/static_cast<float_t>(dt));
    mObj->mVert  += static_cast<float_t>(dy) * (sSense/static_cast<float_t>(dt));

    glm::quat q_rotate;
    glm::vec3 direction = glm::vec3(0,0,200.0);
    glm::vec3 up = glm::vec3(0,1,0);

    q_rotate = glm::rotate( q_rotate, mObj->mHoriz, glm::vec3( 0, 1, 0 ) );
    q_rotate = glm::rotate( q_rotate, mObj->mVert, glm::vec3( 1, 0, 0 ) );

    direction = q_rotate * direction;
    up = q_rotate * up;

    mObj->mViewMatrix = glm::lookAt(direction, glm::vec3(0,0,0),up );

Quite simple eh? mViewMatrix can now be sent to our vertex shader. If you take a closer look at our shader you can see *mMVPMatrix*. This matrix multiples all the vertices and we end up with our lovely scene.

This is quite a brief introduction really. I'm still re-learning all of this. I find it quite useful to get my head around the various shaders and buffers because this is exactly how WebGL works (as that is basically OpenGLES2). More to come!
