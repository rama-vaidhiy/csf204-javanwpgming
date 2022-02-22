# Lab 7

In this lab, we will look at another Java Program which will uses a Two-way Communication between Client and Server using TCP.
 
Your task is to create a **Rock Paper & Scissors game** using Java Networking. The requirements are as follows:
 
a.   The server class will start with a pre-defined port and wait for the clients to connect.

b.   There should be exactly two clients that are allowed to connect to the server. Any more should be sent an error code 403 – Forbidden Service.

c.   The clients will establish a connection with the server with a message named HELO. Any other message should be ignored by the server and sent the error code 402 – Incorrect SYN message.

d.   When the server receives the HELO message correctly, it should send an acknowledgement message to the client which is 200 – OK.

e.   Once the client receives the 200-OK message then it should ask the user to choose between Rock (R), Paper (P), & Scissor (S). It should be only one of those options. Any other option should be responded as an incorrect option and should prompt the user to enter the correct input.

f.     Once the Server receives the inputs from both the clients, it should evaluate the winner and send the YOU WIN message to the winning client and YOU LOSE message to the losing client. If it is a draw, then the server should send TIE to both the clients.

g.   Once the results are transferred from the server to the client, the server should send a 500-BYE message code to the clients and close their streams and wait for the next two clients to start the game.

h.   The Clients on receiving the 500-BYE message should print “End of game” to the user and end the program.

**Rules of the game**

|Inputs|	|	Outputs	 | |
|---|---|---|---|
|Client|	Client2|	Client1	|Client2|
| R	| R | 	TIE | 	TIE| 
| S	| S | TIE| 	TIE| 
| P | 	P| 	TIE	| TIE |
| R |	S	 |YOU WIN |	YOU LOSE |
| S |	R	 | YOU LOSE	| YOU WIN |
| R |	P | YOU LOSE |	YOU WIN |
| P |	R |	YOU WIN	|  YOU LOSE |
| S |	P	 | YOU WIN |	YOU LOSE |
| P |	S	| YOU LOSE |	YOU WIN |
