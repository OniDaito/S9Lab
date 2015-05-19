--- 
layout: post
title: Quartz Composer Programming
tags: programming
introtext: I've been asked by a client to work on a set of patches for Quartz Composer. I was quite chuffed really because it meant playing with Shadows and other suchs cool things.
strapline: Quartz Composer is odd!

---

![quartz](http://4.bp.blogspot.com/-FoRqxMeqWLY/TYys6hW_pXI/AAAAAAAAAyU/mv9YXumOqxo/s320/qc.png)


I've been asked by a client to work on a set of patches for Quartz Composer. I was quite chuffed really because it meant playing with Shadows and other suchs cool things. What I didnt know was that there quite a lot of problems with programming in QC. There is the Apple official way which is quite well documented and then there is the <a href="http://kineme.net/release/QCPatchXcodeTemplate/10">SkankySDK</a> way which is sort of unofficial and a hack.


The thing is, I should have realised it was a hack. Looking at the Kineme webpage though, and the fact that you have to pay for things made me feel that this was usable by any old dev. Not so. The <a href="http://kineme.net/release/Kineme3D/12">Kineme3D</a> and other plugins allow a lot of extra functionality within QC such as model loading and all the rest. Now thats just what we need. If one could create a <span style="font-weight:bold;">Macro Patch</span>, one could then add things with Depth of Field and Fog or whatever to your sub patches.
Apple doesn't let you program Macro patches.


Bummer! So that means we need to use the SkankySDK from the Kineme webpage after all. Sadly, there is no documentation and almost no comments in the headers! Unbelievable! Im still annoyed about that. Also, the examples included in the SDK are slightly misleading.
So, there are 3 patch types in Quartzcomposer. One creates values, one passes values and the final one renders. These are called *Consumer patches* and it is one of these I wanted to right. Turns out you need to make sure that this class (inheriting from QCPatch) returns the correct execution method and that it has no outputs! Sounds obvious that an end-of-the-line patch should have no outputs but you need to make sure, otherwise QC wont let you use it.


Also, all output and input ports as they are known *must have their variable names start with either input or output*. This is mentioned anywhere on the SkankySDK (maybe this is mentioned on Apple's site) but thats a massive failure in my opinion.
Consumer plugins allow you to write OpenGL basically. So all your standard Shader and FBO commands can be written inside a consumer. But there are a couple of things you need to do first. Any file that makes reference to OpenGL needs to include:

    import <opengl/gl.h>
    import <opengl/opengl.h>
    import <opengl/cglmacro.h>

Now, you might think that is obvious, but the the program will compile and appear to run even without these import lines. If you put them in, your patch will work. If you miss them out, you patch will execute its children but not work itself. How crazy?


In addition, any OpenGL function needs this line:

    CGLContextObj cgl_ctx = [context CGLContextObj];

Why? I have no idea yet!
So, is that it then? No, there is one last thing. You need to be careful with the execution of subpatches:

    [executeSubpatches:time arguments:arguments];

This executes your subpatches for you which works fine but remember that you have no control on state. You should, as a best practice, push and pop all you need to and nothing else. So inside my FBO code  I don't include a clear statement because there is another patch that does that for me.