# Introduction #

This document will hopefully show how to make simple tcp hole punching connections through the network.

# Details #

There are two hosts involved in this setup. Local host will be referred to as "local", the remote host will be referred to as "remote." The required software is netcat and hping2. There needs to be 2 terminals open on the "local" machine. These will be referred to as "local1" and "local2". The procedure is as follows:

Tell the local machine to start listening for a TCP connection at port 14141.

` local1:~$ nc -l -p 14141 `

In the second window of the local machine, ready the outgoing connection. Here "remoteIPAddress" is the external IP address of the remote machine. Simply type this command but do not execute until we have setup the remote machine.

` local2:~$ sudo hping2 -c 10 -S -s 14141 -p 1153 remoteIPAddress `

On the remote machine we need to send the desired message to the local machine. Here "localIPAddress" stands for the external address of the local machine. Ready this command but do not execute it yet.

` remote:~$ sudo echo "hello" | nc -p 1153 localIPAddress 14141 `

All ready? If so, execute local2's command first, followed by remote's command. Hopefully you will see "hello" appear in local1's window. You have just successfully punched a tcp hole.

# Notes #

A similar tutorial exists for UDP hole punching [here](http://www.heise-online.co.uk/security/How-Skype-Co-get-round-firewalls--/features/82481/1)