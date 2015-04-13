Title: networked snake
date: 2013-10-10
---

I built snake in Python in the Spring (2013) and I just recently finished the server. I built the server on top of TCP, but Python 3's built in TCPServer class was too heavy for my purposes. Interfacing with Python 3's BSD Sockets library led to a much clearer architecture for the server. This was my first experience with BSD Sockets and I can't believe how well designed they are. I decided to make the client (also written in Python) as thin as I could, so it literally receives coordinates from the server and draws them on the screen. The server handles all the game logic.  The thin client model is much more robust and less error-prone, and should make it easier to write an HTML5 client so players don't have to download any software to play.

The server's pretty fragile &amp; laggy right now. I'm going to make it more robust in the coming weeks.

You can download the code <a href="http://github.com/samertm/snake-python">here</a>.
