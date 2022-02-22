# Lab 1

## Aim:
	To get the ip address of a host. 

## Theory:
	For this lab we will be using the InetAddress API provided by Java's networking package (java.net.\*). It is a class in Java which represents an Internet Protocol (IP) address. An instance of an InetAddress consists of an IP address and possibly corresponding hostname. The class represents an Internet address as Two fields: 
	
  1. **Host name** = Contain the name of the Host.
	
  2. **Address** = The 32 bit IP address. 
  
	For e.g. swansea.ac.uk/137.44.60.150
	
  These fields are not public, so we can’t access them directly. There is not public constructor in InetAddress class, but it has a few static methods that returns suitably initialized InetAddress objects. We are interested in the following:
  
  > **getByName(String host)** - Determines the IP address of a host, given the host's name.
  
 > **getLocalHost()** - Returns the address of the local host.
	
  > **getLoopbackAddress()** - Returns the loopback address.
  

## Task:

You task is to create a Java Program that will use all the three above mentioned API's to get the InetAddress of the following and print the IP Address using the appropriate API's. 
		
    a. Find the IP address of www.who.int.
		
    b. Find the local IP address of your machine.
		
    c. Find the loop back address of your machine. This should be similar to what you identify using ipconfig/ifconfig.
