# 35C3 Junior CTF
# Web write-up - Mc Donald

This is a write-up for one of the first web challenges in the 35C3 Junior CTF - Mc Donald

   
This was the tip:
> -   Our web admin name's "Mc Donald" and he likes apples and always forgets to throw away his apple cores..
    http://35.207.91.38


/robots.txt had the following:

    User-agent: *
    Disallow: /backup/.DS_Store
 
I digged around for a bit reading more about this .DS_Store file and concluded that this is an automatically created file in MacOS that saves meta-information about a certain directory like icons, size, other directories, etc.

In this search I also came across some parsers for this kind of file, i used [gehaxelt's Python-dsstore](https://github.com/gehaxelt/Python-dsstore).

This was the output:

![https://i.imgur.com/NToTuLN.png](https://i.imgur.com/NToTuLN.png)

I tried to navigate to 
>http://35.207.91.38/backup/a

>http://35.207.91.38/backup/b

>http://35.207.91.38/backup/c

But the access was forbidden.
My next idea was to try and find other DS_Store files inside these directories and bingo. 
Kept digging through the directories' DS_Store files and running them through the python script until I reached this one:
http://35.207.91.38/backup/b/a/c/.DS_Store

![enter image description here](https://i.imgur.com/MnQyh9i.png)

Finally, tried to reach:
>http://35.207.91.38/backup/b/a/c/flag.txt

it's a hit

>35c3_Appl3s_H1dden_F1l3s


