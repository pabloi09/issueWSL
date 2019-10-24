# The problem
I have been struggling with a proxy network problem for a long time now that has been driving me nuts. I was developing with the following tools:

-Windows subsystem linux (WSL)

-Visual Studio Code (with remote WSL extension)

-A localhost server for developing apps. In my case a React localhost and a React Native expo host

-Google Chrome

After some time coding I lose internet connection with error codes as ERR_CONNECTION_REFUSED and similar. The Windows' troubleshooting display the message: "Windows could not automatically detect this network's proxy settings"

<img src="https://github.com/pabloi09/issueWSL/blob/master/message.jpg?raw=true"/>

I only get connection back with a reboot. I you are having a similar issue, this is (probably) the post you were looking for.

# The cause
After a lot of time lost, I discovered that if I killed the tasks associated with my development context I solved the problem. I haven't digged more into it, but it could be only one of this tasks or it could be the use of them together. My hypothesis is that for some reason these programs overcharge the network card and the web browser can't access it (all the ports get locked)

# The solution
I would call it more a reduction of the impact of the issue that a solution. We can just kill the tasks with the task administrator program. But that's slow... It is probably faster to reboot the computer. 

But luckily, we are programmers! So let's automatize the task as much as possible. First we could create a .bat script that kill all of these tasks

```
taskkill /im "Code.exe" /f
taskkill /im "init" /f
taskkill /im "node" /f
taskkill /im "wslhost.exe" /f
taskkill /im "bash.exe" /f
taskkill /im "conhost.exe" /f
taskkill /im "Hyper.exe" /f
```
Note: I use the  terminal with Hyper but you should kill your tasks associated with the terminal you are using

Now you just need to execute this script with admin user as follow:
```
runas /profile /user:<your user> "<the path of the .bat>"
```

It will ask you your password and... you will be done! You recover your internet connection. Of course, I am sure there are more elegant an efficient solutions: do a while loop with all the tasks you want to kill(less code), automatically detecting the lost of the internet and executing the script in consequence...but this works for me

If we just create a .bat file with this second command we will be able to double click it and write our user password and we will have all the work done 

# Pro tip: Make it an exe file so you just neet to open it like a program 
So I came into this code https://github.com/npocmaka/batch.scripts/blob/master/hybrids/iexpress/bat2exeIEXP.bat by npocmaka. This script allows you to drag a .bat file and drop it into this other .bat file. It will automatically convert it into a .exe file.

<img src="https://github.com/pabloi09/issueWSL/blob/master/showing.gif?raw=true"/>

Now create a direct access to this exe and set it a beautiful icon. You will have access to your script with a click!

<img src="https://github.com/pabloi09/issueWSL/blob/master/demo2.png?raw=true"/>






