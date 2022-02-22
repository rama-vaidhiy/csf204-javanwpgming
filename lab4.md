# Lab 3

In this lab, we will look at another Java Program which will simulate a Client Server model of communication.

## A Simple Threaded Server

The previous example was pretty trivial: it did not read any data from the client, and worse, it served only **one client at a time**.

This next server receives lines of text from a client and sends back the lines uppercased. It efficiently handles **multiple clients at once**: 

When a client connects, the server spawns a thread, dedicated to just that client, to read, uppercase, and reply. The server can listen for and serve other clients at the same time, so we have true concurrency.

Try writing a Server Program on your own using the previous one as an example.

Here is a detailed description of what it should do.

_Hint:_ We need to implement Runnable to ensure that it runs all the time accepting multiple requests.
```
import java.io.IOException;
import java.io.PrintWriter;
import java.net.ServerSocket;
import java.net.Socket;
import java.util.Scanner;
import java.util.concurrent.Executors;
Import java.util.concurrent.ExecutorService;

/**
 * A server program which accepts requests from clients to capitalize strings. When
 * a client connects, a new thread is started to handle it. Receiving client data,
 * capitalizing it, and sending the response back is all done on the thread, allowing
 * much greater throughput because more clients can be handled concurrently.
 */
public class CapitalizeServer {

    /**
     * Runs the server. When a client connects, the server spawns a new thread to do
     * the servicing and immediately returns to listening. The application limits the
     * number of threads via a thread pool (otherwise millions of clients could cause
     * the server to run out of resources by allocating too many threads).
     */
    public static void main(String[] args) throws Exception {
        try (ServerSocket listener = new ServerSocket(59898)) {
            System.out.println("The capitalization server is running...");
            ExecutorService pool = Executors.newFixedThreadPool(20);
            while (true) {
                 pool.execute(new Capitalizer(listener.accept()));
            }
        }
    }

    private static class Capitalizer implements Runnable {
        private Socket socket;

        Capitalizer(Socket socket) {
            this.socket = socket;
        }

        @Override
        public void run() {
    //Implement the method where we accept the string and convert it to capital case.
           }
    }
}

```

In order to implement the method in the server, you need to understand about the Streams and how the server will read from the socket's stream and how it will output the response to the socket's stream. Don’t rush to do the code. Do some reading on it before you tackle it. 

Sockets have two streams. One for Input and one for Output. Decide on which one should you be using for reading and which one for writing the result back. Check the previous lab task and see how it was done.

Before writing a client, test with nc (in Linux/Mac). Our server reads until standard input is exhausted, so when you are done typing in lines, hit Ctrl+D (clean exit) or Ctrl+C (abort):

```
$ nc 127.0.0.1 59898
yeet
YEET
Seems t'be workin'
SEEMS T'BE WORKIN'
```

Now for a pretty simple command line client:

```
import java.io.IOException;
import java.io.InputStreamReader;
import java.io.PrintWriter;
import java.net.Socket;
import java.util.Scanner;

public class CapitalizeClient {
    public static void main(String[] args)  {
        if (args.length != 1) {
            System.err.println("Pass the server IP as the sole command line argument");
            return;
        }
        try (Socket socket = new Socket(args[0], 59898)) {
            System.out.println("Enter lines of text then Ctrl+D or Ctrl+C to quit");
            Scanner scanner = new Scanner(System.in);
            Scanner in = new Scanner(socket.getInputStream());
            Writer out = new PrintWriter(socket.getOutputStream(), true);
            while (scanner.hasNextLine()) {
                out.println(scanner.nextLine());
                System.out.println(in.nextLine());
            }
        }catch(Exception)
{

}

    }
}
```

This client repeatedly reads lines from standard input, sends them to the server, and writes server responses. It can be used interactively:

```
javac CapitalizeClient.java 
java CapitalizeClient localhost
Enter lines of text then Ctrl+D or Ctrl+C to quit
hello
HELLO
bye
BYE
```

## Task:

Update the server code. Try to create more than one terminal which runs the client and see if the server responds to each client separately. Add screenshots of multiple clients responding to server separately. This program is about multi threading and the server responding to more than one client at the same time. Try to test that aspect and see if it works.

## Challenge Task:
For the challenge task to take this task forward simulate th  following:

Client ----------> Requests for a file (can be any file) -----> Server
Server ---------> Locates the file in its directory and sends it back to the client -------> Client
Client displays the contents of the file on the terminal or saves it to its current directory as a file.

Add error conditions to your code (e.g. file not found, unable to read the file as it is not supported by server etc.)

_Again, the aim of this task is to introduce the concept of server serving multiple clients using threads._
 
