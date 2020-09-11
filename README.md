Hava Kantrowitz
CS3700
Project 1 Readme 

High Level Code Approach 

My code is written in Python and broken up into methods. A detailed description of each method can be found in comments within the code, but here is a quick overview: 
 - User runs the client program, triggers main method
 - Main method calls init\_parsing(), which handles command line parsing and basic user error checking, returns given arguments in a list 
 - Main method calls run\_protocol(), which creates the socket and sends the HELLO message 
 - run\_protocol() calls get\_data(), which receives the message from the server and handles basic error checking, then calls get\_count(), which returns the count of the specific symbol in the random string
 - run\_protocol() calls next\_protocol(), sending it the socket and the count
 - next\_protocol() sends the COUNT message to the server, and calls get\_data() to receive and process the return message
 - If next\_protocol() receives another FIND message, it continues recursively
 - If next\_protocol() receives a BYE message, it closes the socket, prints the secret flag, and returns successfully
 - If next\_protocol() receives a malformed message, it returns an error of -1

Challenges Faced

I've never really heard of sockets in a computer-science related manner before, much less programmed anything involving one, so this project was completely new to me. Reading through Beej's guide helped me understand what sockets were and why they were relevant/necessary to this course. I also faced a few challenges in actually working with the code:
 - It took me a while to figure out how to properly read and process the data from the socket. I was reading it and looking for the newline, but I couldn't seem to see the newline even when it was there. I figured out that this was because I wasn't reading the data from the socket as ASCII, once I added that I was able to properly read and process the data from the socket. 
 - Related to the above issue, since I wasn't reading in the message properly I also wasn't counting properly, and that lead to quite some time debugging my counting code, which ended up not being an issue 
 - In handling the SSL, I ran into an SSL: CERTIFICATE\_VERIFY\_FAILED error. After googling, I determined this to be because the server has a self-signed certificate, and adapted my code to handle this. 

Testing Overview

I didn't do formal unit testing for this project. Instead, I called the program with different combinations of inputs and manually verified that it behaved as expected in each case. 

Sources Consulted
Beej's Guide to Network Programming 
Socket Programming in Python (realpython.com/python-sockets/#socket-api-overview)
TLS/SSL wrapper Python documentation (docs.python.org/3/library/ssl.html)
A few StackOverflow posts to look up specific error messages
