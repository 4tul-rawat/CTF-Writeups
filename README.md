# Portswigger — Web Security Academy — CSRF where token validation depends on the token being present

Hello everyone,

Greetings,

In 2019, Acunetix conducted a study that discovered the presence of CSRF vulnerabilities in 12% of the web applications that were tested. Although the impact of this vulnerability may not be as prevalent nowadays, it is important for everyone to be aware of it, as well as its potential impact. I came across an excellent resource, the Portswigger Web Security Academy, which provides labs designed to help you understand web application security flaws. Today we are going to look at a basic CSRF exploitation from the same lab.

In simpler terms, when a web server is designed to receive a request from a client without any mechanism for verifying that it was intentionally sent, then it might be possible for an attacker to trick a client into making an unintentional request to the web server which will be treated as an authentic request. This can usually be done via a URL, image load, XMLHttpRequest, etc. and can result in exposure of data or unintended code execution.


