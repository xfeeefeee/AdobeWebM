AdobeWebM
=========

> This is a project where I'm building plug-ins for Google's [WebM](http://www.webmproject.org/) format to be used inside the various Adobe applications.

This version has been forked from an earlier version of AdobeWebM https://gitlab.com/fnordware/AdobeWebM/ (formerly https://github.com/fnordware/AdobeWebM ) in order to add fixes to vp9/vp8 import where quantization errors in timestamps can lead to specific frames occasionally never being 'found' and Adobe Premiere or After Effects hanging while trying to find them. For example, converting the requested timestamp from Adobe's internal to mkv/webm format may end up calculating frame number [..., 110, 110, 112, ...] and Adobe gets upset waiting for frame 111 to exist. Additionally, due to the nature of no inherent framerate / there are just timestamps on each frame, the duration calculation can be incorrect, leading Adobe to wait for a frame at the end that may never come eg requesting frame 330 but only getting [..., 328, 329] etc.

I experimented with adding support for the Async Importer interface, but there is very little documentation or examples on this, and despite theoretically working, still ran into weird issues, so that is disabled.

This is an earlier version that does not support the AV1 codec, nor use the hardware acceleration libraries added in current versions of AdobeWebM. I'm only making this available because without my fixes, this plugin is unusable for video editing with many WebM sources. An unscientific analysis of a few hundred WebM clips shows that about 50% of them would fail or hang due to this situation; thankfully none hang or fail after my changes. This may be less likely if using higher or more consistent quality sources as compared to random vp9 videos from who knows what encoder.

Note that I changed this project to use vcpkg rather than try to deal with building a bunch of git submodules.


Download
--------

If you need only vp9/vp8 webm import without hangs, then use one the releases in this github repo. Otherwise [get the official WebM plug-in on fnordware.com](http://www.fnordware.com/WebM/) for AV1 support and hardware acceleration (but without these fixes for now)


Install
-------

Copy to eg `C:\Program Files\Adobe\Common\Plug-ins\7.0\MediaCore`


License
-------
BSD


Author
------
Brendan Bolles
+ minor fixes in this fork by xfeeefeee
