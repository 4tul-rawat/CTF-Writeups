# Portswigger — Web Security Academy — CSRF where token validation depends on the token being present

Hello everyone,

Greetings,

In 2019, Acunetix conducted a study that discovered the presence of CSRF vulnerabilities in 12% of the web applications that were tested. Although the impact of this vulnerability may not be as prevalent nowadays, it is important for everyone to be aware of it, as well as its potential impact. I came across an excellent resource, the Portswigger Web Security Academy, which provides labs designed to help you understand web application security flaws. Today we are going to look at a basic CSRF exploitation from the same lab.

In simpler terms, when a web server is designed to receive a request from a client without any mechanism for verifying that it was intentionally sent, then it might be possible for an attacker to trick a client into making an unintentional request to the web server which will be treated as an authentic request. This can usually be done via a URL, image load, XMLHttpRequest, etc. and can result in exposure of data or unintended code execution.

Tools Required —

BurpSuite (You don’t need a Pro version, I have used the community version for this lab).

Let’s dive into solving this lab.

Login to the Portswigger web security academy lab and look for this lab under the CSRF section. To solve this lab we need to create a CSRF Proof of Concept that changes the email address of the victim (wiener:peter in this case) and upload that to the exploit server. Click on “Access the lab” and log in using the given credentials.

![image](https://github.com/4tul-rawat/Writeups/assets/130515502/ec32acff-78c2-4d4b-9a72-0133d5859827)

Once you access the lab using the given credentials, an update email functionality will appear. This is the feature that we need to exploit. in the lab and we need to create a CSRF proof-of-concept for this.

![image](https://github.com/4tul-rawat/Writeups/assets/130515502/b12405c4-8634-4c5f-b665-4ac203901e9c)

Here comes the role of BurpSuite. Burpsuite is a tool that is utilized for intercepting and modifying requests before sending them to the server. This is one of the most powerful security tools available and is highly used by penetration testers to find security bugs in the applications.

Let’s open Burpsuite now and intercept the request associated with the update feature. Here I am trying the change the email address to some random email address(in a real scenario, this can be an attacker’s email).


As you capture the request in the Burpsuite, you will notice that the browser or client sends a post request with two parameters in the body of the request — an email and a csrf token. A csrf token is one way to check if the request is coming from an authenticated user and is widely used to check the authenticity of any action.

Let’s send this request to the repeater(Ctrl+R) and make some modifications to the request.

Let’s try to capture the response by removing the value in the csrf token. Once you do that, you will see the response as “invalid csrf token”.


Now, let’s try to send an empty csrf token. Once again, it shows “invalid csrf token”.


What about modifying a csrf token value? Let’s try that. It didn’t work either.


Let’s try one more time and this time, I am completely removing the csrf token as if it never exists. Amazing, it worked! We got 200 okay response. I can see the modified email on the response page.


So what exactly is happening? Let’s understand this. In this case, the server is checking two cases, 1) Either the token has to be valid or 2) in the absence of a token, the server is not checking for one at all. We can leverage this to create a csrf poc and exploit this functionality.

Let’s create a proof-of-concept now. I am also learning so I try to create proof-of-concept on my own and the proof-of-concept for this is not that complicated. Basic knowledge of HTML tags and JavaScript would work.

Once you create the proof-of-concept, open the exploit server and paste your proof-of-concept in the body section. Click on “Store” and then “View Exploit”. If the email changes, then your proof-of-concept is working as expected. Now, you can choose the option “Deliver Exploit to Victim”.



This is my first medium post and I would appreciate any feedback that would help me improve my content or suggestions for any next topic that you want to learn.
Keep Hacking!


