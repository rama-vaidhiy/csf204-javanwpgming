# Lab 6

As part of this lab, we shall simulate the **CSMA/CD algorithm** which is used in the Ethernet standard of LAN.

The algorithms for both the server and client are provided. 

**Server Algorithm:**

1. Initialize the server socket (choose any allowed ports) 
2. Display waiting for connection 
3. Once the client sends a request, accept the connection.
4. Display the message that the client has been connected.  
5. Initialize the input stream of the socket.
6. Read the message.
7. Display message from the client's stream and display it on the screen.
8. Close all connections. 
9. Stop the program.
 

**Client Algorithm:**

1. Open the socket with input address ,port (make sure to use the correct port of the server)
2. Initialize the output stream
3. Send the message (any random message)
4. If the message is sent successfully, then there is no collision. 
5. If message is not sent, assume that the collision has occurred (To simulate collision, run the client without running the server)
6. Calculate backoff time using random number and wait for that time using Thread.sleep. Algorithm is given below.
7. Again send the message, if message is sent then collision has not occurred. (Do not start the server yet)
8. If message not sent, then collision has occurred, Go back to step 6. Repeat the process for 15 times. 
9. If not succeeded with 15 attempts, then the transmission will be stopped.

 

**Backoff time calculation:**

Number of attempts: 15

Waiting time chosen t: 2000 ms

For every attempt:

	Random number  r = any number between (0, ( 2 ^ attempt number ) - 1)
  
	Time to wait before next attempt = t * r


**How to simulate the program:**

	a. Do not run the server code first
	b. Run the client code on its own. It should try and send the message. It will definitely be unsuccessful (because the server is not running)
	c. The client should wait for the backoff time calculated and retry the message on its own.
	d. Let the client try to send the message for at least 5 attempts. 
	e. During the 6th attempt, start the server. 
	f. Once the 6th backoff time is done, the client will automatically connect to the server and the server will print the message from the client and both the programs will end.

Copy paste your Client and Server code along screen shots of your execution. 
