# Lab 8

In this lab, we will look at UDP client and server using DatagramSocket and DatagramPacket. Unlike the TCP which is connection-oriented, UDP is connection-less.
 
Sample UDP Server and Client Code for reference. 

 ```
//UDP Server
import java.io.*;
import java.net.*;
 
public class UDPServer
{
 
    public static void main(String args[]) throws Exception {
        //Create the UDP Socket
        DatagramSocket serverSocket = new DatagramSocket(9876);
        //Define the bytes that can be received
        byte[] receiveData = new byte[1024];
        //Define the bytes that can be sent
        byte[] sendData = new byte[1024];
        while(true) {
            //Create empty Packet
            DatagramPacket receivePacket = new DatagramPacket(receiveData, receiveData.length);
            //Receive the packet
            serverSocket.receive(receivePacket);
            //Conver the packet to a string
            String sentence = new String( receivePacket.getData());
           
            //Get the address of the Client from the packet received
            InetAddress IPAddress = receivePacket.getAddress();
            //Get the port of the Client from the packet received
            int port = receivePacket.getPort();
            //Print it out
            System.out.println("RECEIVED TEXT: " + sentence);
            //Capitalize it
            String capitalizedSentence = sentence.toUpperCase();
            //Get the bytes ready
            sendData = capitalizedSentence.getBytes();
            //Create a Datagram Packet with the capitalized data that was sent
            DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, port);
            //Send the packet
            serverSocket.send(sendPacket);
        }
    }
}
```
 
 
 ```

//UDP Client
import java.io.*;
import java.net.*;
import java.util.Scanner;
public class UDPClient{
    public static void main(String args[]) throws Exception {  
        //create the scanner   
        Scanner inFromUser =new Scanner(System.in);
        //Create a client socket
        DatagramSocket clientSocket = new DatagramSocket();
        //get the IP address
        InetAddress IPAddress = InetAddress.getByName("localhost");
        //set the sending byte length
        byte[] sendData = new byte[1024];
        //set the receiving byte length
        byte[] receiveData = new byte[1024];
        //get the input from the user
        String sentence = inFromUser.nextLine();
        //convert it to bytes
        sendData = sentence.getBytes();
        //create the packet with the input
        DatagramPacket sendPacket = new DatagramPacket(sendData, sendData.length, IPAddress, 9876);
        //send the packet
        clientSocket.send(sendPacket);
        //Create a packet for receiving
        DatagramPacket receivePacket = new DatagramPacket(receiveData,receiveData.length);
        //receive the packet
        clientSocket.receive(receivePacket);
        //get the modified data from the server
        String modifiedSentence = new String(receivePacket.getData());
        //print the message
        System.out.println("FROM SERVER:" + modifiedSentence);
        //close the socket
         clientSocket.close();
    }
}
 
 ```
 
## Task: 

Run the above program to see what the Client and Server do and how they communicate. Did it work as it should?

Answer:
```


```


Explain the differences you notice between the TCP way of communication of the same program and the UDP (the above program) way of communication. (API's used, the way the connection is established etc.) 

Answer:
```



```




## Challenge Task: 

Once you have run the above programs, change them to do the following:
 
**Server:**

	1. Create a file (not a java file) and call it quotes.txt.
  
	2. Add a few quotes (more than 3) of your choice to this file.
  
	3.  The Java UDP Server program should do the following:
  
		a. When the receive function is called, load a random quote from the file (it is entirely up to you to how you want to do this).
    
		b. Send the random quote to the client using the send function.
 
**Client:**

The Java UDP Client should do the following:

	1. It should not accept any input from the end-user.
  
	2. When it connects to the UDP server, it should send an empty packet.
  
	3. When it receives a packet from the server, it should display the contents to the end-user.
  
	4.  Sleep for a couple of minutes and connect to the server to receive another quote.
  
	5.  Quit after receiving three quotes.
