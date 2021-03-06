# Scribe
A Chrome extension that converts raw text URLs in Gmail to embedded images or to friendly hyperlinks with page title text, like Quora's text editor. I'm doing this because it's fun, and I really want to improve system designs. 

# Back-End

- A server that contains a Python crawler. On receipt of a URL, the crawler fetches the associated page and parses it for important human-readable information (a title tag or similar). If the URL points to an image file, it simply downloads the image. 
- Current design of system employs use of a self-designed HTTP server with support for only a GET request for handling communications. An HTTPS wrapper provided by Mashaope's convenient API functionality allows us to access this point from an HTTPS endpoint.

# Front-End

A Chrome extension that encodes an event handler on pressing the F2 key in the document window (rather than a compose window). An XMLHttpRequest is carried out synchronously, and the result replaces the URLs. 

# Current Status

**This Chrome extension is able to reproduce all the desired functionality.** Pressing the F2 key in the document window once converts all raw URLs to human-readable links and actual images. All that's left is to iron out a few kinks that would subtract from user experience (see Issues).

The back-end server is complete, with an HTTPS middleman ensuring security. Current example of API endpoint definition can be seen in `server.py`. One can view examples within a favourite browser - the server has been successfully daemonised, and runs continuously on port 8080 of my domain.

The front-end component is nearing completion. It uses [Autolinker.js](https://github.com/gregjacobs/Autolinker.js) to grab all raw URLS and implements a simple XMLHttpRequest to communicate with the server. Currently this XMLHttpPRequest works synchronously (i.e. the document will wait until the request is handled), something I plan to fix soon (this does mimic Quora's behaviour, but that is no excuse for embracing deprecated functionality). It replaces the text in a compose or reply window with nice hyperlinks and images.

# Current Issues

* The F2 can only be pressed in the document window - it will not work if focus is on the composition or reply window. One should ideally focus on the compose or reply window that the user is on, and allow the application to affect that window.


Efforts are being made to resolve this.
