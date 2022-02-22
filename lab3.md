# Lab 3

## Aim: 
To implement a simple Client-Server program.
 
## Theory: 
We will look at a simple Java Program which will simulate a simple one-way communication. The server sends data to the client only.

Ensure to run the server and the client in the same system for now in different command prompts / terminals.

_Replace the var with the appropriate Class definition in the code, if you are using java version < 10._
 
### A Trivial Sequential Server

This is perhaps the simplest possible server. It listens on port 59090. When a client connects, the server sends the current datetime to the client. The connection socket is created in a try-with-resources block so it is automatically closed at the end of the block. Only after serving the datetime and closing the connection will the server go back to waiting for the next client.
```
//DateServer.java

import java.io.IOException;

import java.io.PrintWriter;

import java.net.ServerSocket;

import java.net.Socket;

import java.util.Date;



/**

 * A simple TCP server. When a client connects, it sends the client the current

 * datetime, then closes the connection. This is arguably the simplest server

 * you can write. Beware though that a client has to be completely served its

 * date before the server will be able to handle another client.

 */

public class DateServer {

    public static void main(String[] args) throws IOException {

        try (ServerSocket listener = new ServerSocket(59090)) {

            System.out.println("The date server is running...");

            while (true) {

                try (Socket socket = listener.accept()) {

		                    PrintWriter out = new PrintWriter(socket.getOutputStream(), true);

                    out.println(inputText.toUpperCase());


                }

            }

        }

    }

}
```

### Discussion:

	• This code is just for illustration; you are unlikely to ever write anything so simple.
  
	• This does not handle multiple clients well; each client must wait until the previous client is completely served before it even gets accepted.
  
	• As in virtually all socket programs, a server socket just listens, and a different, “plain” socket communicates with the client.
  
	• The ServerSocket.accept() call is a BLOCKING CALL.
  
	• Socket communication is always with bytes; therefore sockets come with input streams and output streams. But by wrapping the socket’s output stream with a PrintWriter, we can specify strings to write, which Java will automatically convert (decode) to bytes.
  
	• Communication through sockets is always buffered. This means nothing is sent or received until the buffers fill up, or you explicitly flush the buffer. The second argument to the PrintWriter, in this case true tells Java to flush automatically after every println.
  
	• We defined all sockets in a try-with-resources block so they will automatically close at the end of their block. No explicit close call is required.
  
	• After sending the datetime to the client, the try-block ends and the communication socket is closed, so in this case, closing the connection is initiated by the server.
 
### Run the server:

You should get the response:
> The date server is running...

If you are using MAC or linux:
To see that is running (you will need a different terminal window):
```
$ netstat -an | grep 59090
tcp46      0      0  *.59090                *.*                    LISTEN
```
Test the server with nc:
```
 $ nc localhost 59090
Sat Feb 16 18:03:34 PST 2019
```
Woah! nc is amazing!

 
Still, let’s see how to write our own client in Java:
```
//DateClient.java

import java.util.Scanner;

import java.net.Socket;

import java.io.IOException;



/**

 * A command line client for the date server. Requires the IP address of

 * the server as the sole argument. Exits after printing the response.

 */

public class DateClient {

    public static void main(String[] args) throws IOException {

        if (args.length != 1) {

            System.err.println("Pass the server IP as the sole command line argument");

            return;

        }

        Socket socket = new Socket(args[0], 59090);
	        Scanner in = new Scanner(socket.getInputStream());

        System.out.println("Server response: " + in.nextLine());

    }

}
```

### Discussion:

On the client side, the Socket constructor takes the IP address and port on the server. If the connect request is accepted, we get a socket object to communicate.
	
Our application is so simple that the client never writes to the server, it only reads. Because we are communicating with text, the simplest thing to do is to wrap the socket’s input stream in a Scanner. These are powerful and convenient. In our case we read a line of text from the server with Scanner.nextLine.

**Test the client:**

> java –cp . DateClient 127.0.0.1

The response in the client window will be:

> Server response: Sat May 16 18:02:35 PST 2020


## Task: 
Convert the above program to ensure that the server sends an interesting quote whenever the client connects to it instead of sending the date. 
Have a text file in the server which contains a list of quotes (interesting) and it reads the file and selects a random quote for every client that it connects. 
