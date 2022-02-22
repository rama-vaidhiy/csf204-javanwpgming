# Lab 9

So far we have been looking at creating a Client Server programs where the server provides a service (quotes/current date etc.) and the client connects to the server and uses the service provided by the server. 

In this lab, we are going to use a well known Client Server mechanism used in our day to day life, the HTTP services.

This was already introduced a little bit earlier where we had a Translator which was using the HTTP URL to talk to WhatsMate's API and retrieve the result from the API.

You will need to know about URLConnection, HttpURLConnection, and URL classes.

A. **URL:** the uniform resource locator which will be used to represent a webpage. This can include just the webpage, a webpage with the file, with an optional port (if it is different in case where you are using your own web server with a different port other than the default 8080 or 80)

B. **URLConnection & HttpURLConnection:** URLConnection is the super class and HttpURLConnection extends from URLConnection. These classes represents the connection between your client and the webpage represented by the URL. You will need to use openConnection (with/without proxy) to establish the connection and using the connection object can then retrieve the streams and use it to send and receive data.

We will be creating a Java Program to connect to a web server which flips a coin and returns a value of heads or tails for you. 

The URL used is http://flipacoinapi.com/txt (_No longer available...you might have to use a different service which returns text_)

There are JSON and XML versions of the same. But for simplicity we will stick with the text format. 

## Task: 

Complete the class below and show the class and its output. 

Add the appropriate import classes	
```
public class URLConnTest{


        private static final String USER_AGENT = "Mozilla/5.0";
        private static final String GET_URL = http://flipacoinapi.com/txt;

        public static void main(String[] args) throws Exception{
                sendGET();
        }

        private static void sendGET() throws IOException{
                //Create an URL object with the given URL
                URL obj = new URL(GET_URL);
                //Create a HttpURLConnection object (look up the URLConnection class)
                HttpURLConnection con = (HttpURLConnection) obj.<what api should be used here>();
                con.setRequestMethod("GET");
                con.setRequestProperty("User-Agent", USER_AGENT);
                int responseCode = con.getResponseCode();
                System.out.println("GET Response Code :: " + responseCode);
                //Based on the response code read the data from the appropriate stream
                //and display the content.
                //do not forget to close the streams and disconnect the connection.
       }
}
```

In the above class, you had a one way communication with the http server. You connected to it and you read the value it returned and printed it in the client application. All this was done using the GET method of the HTTP.


Now, in order for a two way communication where you send a value to the server and get the response back, we need to use the POST method of the HTTP. Using POST, you need to send the values to the HttpUrlConnection Object's stream.

Modify the above code to send the username and password to a test website and read its response.

> The URL is: http://testing-ground.scraping.pro/login   

>Parameters to be passed are:  
>					usr=admin
>					pwd=12345

