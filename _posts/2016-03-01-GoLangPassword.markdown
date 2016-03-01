---
layout: post
title: Writing a password management page in Go 
introtext: I've been meaning to play around with Go for a while. A project came across my desk that was just perfect for getting to grips with this modern language  
strapline: Using Go in Anger for a Password Management page
tags: programing work golang web
---

I've been meaning to play around with [Go](https://golang.org) for a while. A project came across my desk that was just perfect for getting to grips with this modern language. We have a webpage at work that allows people to change their passwords for the cluster and for their samba shares. It's an important but small program that was previously written in Perl. The existing source was quite old and had been changed a fair bit over the years. After looking at it for quite some time, I figured I'd learn some Go and start from scratch. I have to say, I'm quite pleased.
introtext: I've been meaning to play around with Go for a while. A project came across my desk that was just perfect for getting to grips with this modern language  

The first cool thing about Go is that it can run as a script, but also as a compiled binary, which is a handy thing indeed. The syntax is quite similar to C in some ways, although the placement of parameters might annoy people if you aren't used to it. Not having classes is a good thing I think; moving away from Object Oriented programing is probably a good thing these days. The second cool thing are all the docs and their associated built-in modules. Go includes lots of lovely things by default. So everything you need to do webserving and such is there. Handlers, FastCGI, URLEncoding and all the rest is there.

One odd thing is the way Go relies on a GOROOT path; a place where Go and all it's projects live. Initially, I wasn't a fan of this but it does make installing extra headers and source really easy. Our password server uses LDAP and this is one thing that isn't in the Go basic install. However, its quite easy to install such things from Github if you've setup your install right. I've been using [go-ldap](https://github.com/go-ldap/ldap) which works a treat. I had to learn a little about [STARTTLS](https://en.wikipedia.org/wiki/STARTTLS) and similar - something i'd come across before with Email along with the basics of [LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol). The best projects are the ones where you get to learn something I figure.

One thing I had to write from scratch were the [ntlmgen](http://perldoc.net/Crypt/SmbHash.pm) functions that create SAMBA hashes. This is pretty outdated stuff but still exists here and there. I lifted some basic code from [here](http://www.codeproject.com/Articles/328761/NTLM-Hash-Generator) but it wasn't great as it failed to support abitrary length strings even though it's quite easy to implement. The code is up at [QMUL Github](https://github.com/QMUL/) if you fancy taking a look. Suffice to say, adding that repos into the GOROOT made the whole library thing quite trivial. 

One problem with Go is how best to deploy it. According to [this page](https://astaxie.gitbooks.io/build-web-application-with-golang/content/en/12.3.html) Go doesn't daemonize readily, which means supervisord or similar needs to be used in order to make sure the program doesn't die unexpectedly. That said, Go supports [FCGI](https://en.wikipedia.org/wiki/FastCGI) out of the box, making talking to Go programs quite easy. With good support for logging I suspect this is a minor inconvenience that will be overcome in future releases. FCGI means that I can use things like '''mod_proxy''' and '''mod_proxy_fcgi''' with [Apache](https://httpd.apache.org/docs/2.4/mod/mod_proxy_fcgi.html) and just a simple directive for testing.

    alias /static /var/www/html/password/static
    
    <location /static>
        Order deny,allow
        Allow from all
    </location>
    
    ProxyPassMatch ^/$ fcgi://127.0.0.1:9001

Vagrant played quite a part in the writing of this software. My boss kindly setup a test server box and dev box, complete with mail server, LDAP and all the services I'd need. One issue we found was that the basic shared directories that [VirtualBox](http://virtualbox.org) provides do not work well with webdevelopment; changing files on a share on the host side whilst the client box was serving them with Apache always resulted in fire and death. Changing these shares to use NFS worked much better. Although I'm a little late to the party on this one, I think using Vagrant and Docker in development is a must these days, though I'll need to figure out a good way to organise my workflow.

[Cracklib](https://github.com/cracklib/cracklib) is something we use here, and that particular library was hacked into the previous Perl script in a nasty way. Go provides a fairly reasonable C Binding called, no surprises, [CGo](https://golang.org/cmd/cgo/). I believe some people are not fans but I actually quite like it. I did have some issues in linking though - I had to resort to using a static library (which is never great and I hope to replace someday). For simple things like this, where one is just passing a pointer to a string around, CGo seems fine. It's great that the designers put this in. Ultimately, C and C++ still underpins most things, and for good reason, so good bindings to it (and hopefully, other languages) is a good thing.

    // #cgo LDFLAGS: /usr/lib/x86_64-linux-gnu/libcrack.a
    // #cgo CFLAGS:
    // #define CRACKLIB_DICTPATH "/usr/share/cracklib/pw_dict"
    // #include <stdlib.h>
    // #include <string.h>
    // #include <stdio.h>
    // char * password_check(char * pw ) {
    //    char const * msg;
    //    char * ret;
    //    msg = FascistCheck(pw,CRACKLIB_DICTPATH);
    //    if (msg){
    //      ret = malloc(sizeof(char) * strlen(msg));
    //      strcpy(ret,msg);
    //    } else {
    //      ret = malloc(sizeof(char) * 5);
    //      strcpy(ret,"GOOD");
    //    }
    //    return ret;
    // }
    //
    import "C"
    import "unsafe"

    func TestPassword(password string) string {
      var cchar *C.char = C.password_check(C.CString(password))
      defer C.free(unsafe.Pointer(cchar))
      return C.GoString(cchar)
    }


Overall I'm quite pleased with how easy Go is to use. It has some odd quirks like forcing you to use all the variables you ever declare, but in the end, it seems like these rules are actually good for you and help you write better code overall. Sadly, the code I've written is internal only at present (and fairly boring) but the snippets here give a flavour of the thing. I'll likely use Go as my goto (hah!) solution for webdev in the future, once I find a good way to daemonize it.


