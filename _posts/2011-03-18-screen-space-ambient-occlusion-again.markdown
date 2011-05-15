--- 
wordpress_id: 115
layout: post
title: ">Screen Space Ambient Occlusion, again!"
wordpress_url: http://www.section9.co.uk/blog/?p=115
---
><object width="480" height="390"><param name="movie" value="http://www.youtube.com/v/4u8lCQ_x-cU?fs=1&amp;hl=en_US"></param><param name="allowFullScreen" value="true"></param><param name="allowscriptaccess" value="always"></param><embed src="http://www.youtube.com/v/4u8lCQ_x-cU?fs=1&amp;hl=en_US" type="application/x-shockwave-flash" allowscriptaccess="always" allowfullscreen="true" width="480" height="390"></embed></object><br /><br />Its a lovely effect, but my research has lead me to two possible versions of this algorithm, based on <a href="http://www.gamedev.net/topic/556187-the-best-ssao-ive-seen/">this thread over at gamedev</a>. I must say, there is quite a lot of good stuff over there and I've had fun reading up on it all. The thing is, its a tricky effect to get right and needs a lot of tweaking. Also, the FPS can take quite a big hit because you need at least 2 geometry passes and 1 SSAO pass to get it to work. With that running, you'll loose a few frames. In addition, you need an accurate depth buffer. I'd forgotten this and it took me ages to track it down. GL_RGBA32F_ARB is your friend.<br /><br />Watch this space, I shall be improving it! :D
