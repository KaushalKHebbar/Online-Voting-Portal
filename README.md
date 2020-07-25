# Online-Voting-Portal

**[Updating Repo . . . . .]**

An e-voting portal using Socket-Programming in Python using IPv4/IPv6.

# Table of Contents

1. [Motivation](#motivation)  
2. [Introduction](#introduction)
3. [Configuration](#configuration)
4. [IPv4 vs IPv6 Addressing](#IPv4 vs IPv6 Addressing)
5. [Communication Workflow](#communication-workflow)
6. [Getting Started](#getting-started)

 
# Motivation
Many countries including India have problems with their voting systems. Considering the huge growth of population in our country, it is not wise to use the “traditional” polling systems where the public must physically be present at the polling booth during the time of casting their votes. The aged and the specially-abled often find it hard to commute to the poll booths and to wait in the long queues. Moreover, the time and money spent on conducting such a large scale operation must be reduced.

As our nation is thriving with digitization, this “Online Voting System” seeks to address the above issues and provides a hassle-free user experience to the electorate.

# Description
In this system, anyone who has registered is eligible to vote from his/her laptop remotely by using his/her mobile hotspot. This enables the electorate to cast his votes from wherever he/she is. A single server is run by the administrator (again using his/her mobile hotspot) and multiple clients (electorates) connect to them using IPv6 addressing This system can be used for a simple from "voting for the best to-go restaurant" to “voting for the best passing out student of the college” !! 

# Configuration
The server and client programs are coded using Socket Programming in Python language. The system is made robust to any kind of sudden power-outage during the live voting session i.e., it does not lose track of the votes already casted. 

## 1. Server configuration
The server is run by the administrator and shall have the following setup:
1.	A laptop/PC connected wirelessly using personal mobile hotspot that is connected to an active GPRS network.
2.	Its Public IPv6. (128 bit address)
3.	A port number common to both server and client.
4.	Python 3.7.x installed along with its IDE. 
5.	The python file named “online_voting_server.py”.
6.	A database of all the registered voters and their passwords in the “Voters_database.txt”
7.	A database of the candidate names in the “Candidates.txt”
8.	A database “Voter_names.txt” having the list of voters already voted.
9.	Finally, a “Votes_record.txt” file containing the polling results after each round.


## 2. Client configuration
The client is run by the electorate and shall have the following setup:
1.	A laptop/PC connected wirelessly using personal mobile hotspot.
2.	Server’s Public IPv6 address.
3.	A port number common to both server and client.
4.	Python 3.7.x installed along with its IDE.
5.	The python file named “online_voting_client.py”.
6.	The username and password provided to him/her.


# IPv4 vs IPv6 Addressing
For IPv4 to communicate with the outside world we need to use Network Address Translation (NAT). This is so because, in IPv4 each device has a private IP address and a private port assigned in its LAN. If one has to connect to a laptop which is connected to the internet through a different LAN using IPv4, then it’s hard to do so, as we can only get Public IP address and public port of that network but not the computer’s Private IP and private port.

This could have been overcome if we had access to the Router for modifying the NAT settings by adding our customized Private IP and port to the Public port mapping. But since we didn’t have the administrator access to do so, the entire procedure was found to be very involved. 

So, we came up with idea of using IPv6 instead of IPv4 itself. In IPv6 addressing, we don’t have Network Address Translation and thus, the concept of Private address doesn’t exist. The laptop gets the same IP address as that of the phone with only the ports changed. This IP address is dynamic and changes every time you turn on your GPRS. The voting Client must be notified about the server IP address. 

The IPv6 address of the PC can be found out by typing *“What is my IP”* on Google Chrome browser or simply the command *“ipconfig”* on the cmd.


# Communication Workflow
The following steps shall be performed by the client and server during the online voting session: (Fig 4.1 summarizes the TCP workflow)
1)	The server shall inform its Public IP to all the clients prior to the voting session. This is done by typing *ipconfig* on the cmd.
2)	The administrator runs the server file by the following command entered on his/her cmd.
           *>> python online_voting_server.py*
3)	Server uses the *socket.socket(socket.AF_INET6, socket.SOCK_STREAM)* function to create a socket. The first argument specifies the Internet address family for IPv6 and the second one indicates TCP sockets used to transport messages in the network layer.
4)	The *bind((host, port))* function associates the socket with a specified network interface and port number on the computer.
5)	The *listen(max)* function enables the server to accept connections and makes it a “listening socket”. The max value specifies the number of unaccepted connections that the system will allow before refusing new ones. (queue length)
6)	At the same time several electorates run the client file by the typing the following command on his/her cmd.
          *>>python online_voting_client.py*
7)	Like the server, the client creates a socket using the *socket.socket(socket.AF_INET6, socket.SOCK_STREAM)* function and uses *connect((host, port))* method to connect to the server.
8)	The *accept()* method in the server blocks and waits for an incoming connection. When a client connects, it returns a new socket object representing the connection and a tuple holding the address of the client. This socket is used to communicate with the client and is distinct from the listening socket that the server is using to accept new connections. 
9)	Hence, the server accepts only one client at a time queuing the rest and mutual communication happens via *send()* and *recv()* methods.
10)	Finally, the connected client closes its connection via *close()* function and the waiting client automatically gets connected to the server. Only after all the clients close, will the server exit.



# Getting Started
### Software and Library Installation


### Steps to follow
1. 

