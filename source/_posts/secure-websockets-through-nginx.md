title: "secure websockets through nginx"
date: 2014-07-10
---

my [snake game](https://samertm.com/snake-mmo-in-golang) works again! It was my first significant effort in go. It's a port of a python program which only handles two connections at any given time. I was able to trivially expand it to work with an arbitrary number of connections in go. That was my first "real" go program.

I used websockets to between the javascript client and the snake-mmo server. Everything broke when I switched to SSL, though, because Firefox refused to send data over a non-secured connection. When I tried upgrading the connection to secure websockets, it broke, and I wasn't sure why. I went through my nginx config a hundred times, but I couldn't understand why nginx wasn't decoding the ssl connection correctly... until I talked to Max about my problem, and he showed me that I wasn't going through nginx at all, and that my server was getting an SSL packet and writing junk in response. So I set up the following in my nginx config to make nginx act as an SSL proxy:

    server {
            listen 4028 ssl;
            keepalive_timeout 70;
            ssl_protocols SSLv3 TLSv1;  
            ssl_ciphers AES1280SHA:AES256-SHA:RC4-SHA:DES-CBC3-SHA:RC4-MD5;
            ssl_certificate /*location of my ssl cert*/ ;
            ssl_certificate_key /*location of my ssl key*/ ;
            ssl_session_cache shared:SSL:10m;                                       
            ssl_session_timeout 10m;
            location / {
                    proxy_pass http://localhost:4027/;
                    proxy_http_version 1.1;
                    proxy_set_header Upgrade $http_upgrade;
                    proxy_set_header Connection "upgrade";
            }
    }

So, my javascript client talks to port 4028, and my snake game talks to 4027. And it works! I'm not sure why the Gorilla websockets client didn't work with ssl connections...
