# Lab 5

In this lab, we will look at another Java Program which will uses a Two-way Communication between Client and Server. 

We will reuse the same files as previous lab but extend it to make a practical application.

We are going to use a Welsh Translator code provided by WhatsMate's Java API's (They have API's for different programming languages too). The API's can be found in the below link.
https://www.whatsmate.net/translation-api.html

The code is given below. 
 
```
import java.io.BufferedReader;
import java.io.OutputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
 
public class Translator {
  // TODO: If you have your own Premium account credentials, put them down here:
  private static final String CLIENT_ID = "FREE_TRIAL_ACCOUNT";
  private static final String CLIENT_SECRET = "PUBLIC_SECRET";
  private static final String ENDPOINT = "http://api.whatsmate.net/v1/translation/translate";
 
  /**
   * Entry Point
   */
  public static void main(String[] args) throws Exception {
    // TODO: Specify your translation requirements here:
    String fromLang = "en";
    String toLang = "cy";
    String text = "Let's have some fun!";
 
    Translator.translate(fromLang, toLang, text);
  }
 
  /**
   * Sends out a WhatsApp message via WhatsMate WA Gateway.
   */
  public static void translate(String fromLang, String toLang, String text) throws Exception {
    // TODO: Should have used a 3rd party library to make a JSON string from an object
    String jsonPayload = new StringBuilder()
      .append("{")
      .append("\"fromLang\":\"")
      .append(fromLang)
      .append("\",")
      .append("\"toLang\":\"")
      .append(toLang)
      .append("\",")
      .append("\"text\":\"")
      .append(text)
      .append("\"")
      .append("}")
      .toString();
 
    URL url = new URL(ENDPOINT);
    HttpURLConnection conn = (HttpURLConnection) url.openConnection();
    conn.setDoOutput(true);
    conn.setRequestMethod("POST");
    conn.setRequestProperty("X-WM-CLIENT-ID", CLIENT_ID);
    conn.setRequestProperty("X-WM-CLIENT-SECRET", CLIENT_SECRET);
    conn.setRequestProperty("Content-Type", "application/json");
 
    OutputStream os = conn.getOutputStream();
    os.write(jsonPayload.getBytes());
    os.flush();
    os.close();
 
    int statusCode = conn.getResponseCode();
    System.out.println("Status Code: " + statusCode);
    BufferedReader br = new BufferedReader(new InputStreamReader(
        (statusCode == 200) ? conn.getInputStream() : conn.getErrorStream()
      ));
    String output;
    while ((output = br.readLine()) != null) {
        System.out.println(output);
    }
    conn.disconnect();
  }
 
}
```

This is a standalone code. 

What will you need?

	a. The above Translator.java code Do not worry about the Translator.java and its API's. We will come those API's later in the module.
  
	b. A copy of the CapitalizeServer code from previous lab.
  
	c. A copy of the CapitalizeClient code from previous lab.
  
Integrate the Translator code in your Server so that when the client sends a text to the server, the server can use the above code to translate it in Welsh and send it back to the client. 

_Note:_

a. You need to make small change to the Translator.java to ensure it can be called from your TranslatorServer.java

b. Your TranslatorServer.java should be similar to CapitalizeServer except it will call Translator.java with the text instead of doing the toUpperCase() on its own. 

c. Your TranslatorClient.java can be exactly the same as CapitalizeClient.java. No change required.


## Challenge Task:

Extend the client code to send the language it wants it to be translated along with the text to be translated. In other words, you should get two inputs from the user
	
  a. The language they want the text to be translated to

  b. The text to be translated

Send both of them to the server. For now, you can set the fromLang to en (English) and only change the toLang to the value given by the client. 






