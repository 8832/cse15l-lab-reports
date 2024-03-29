# Lab Report 2
By: Sara Standlee
## Part 1
Below is the code for a web server called `ChatServer`. There are four java classes for this server. \
First, in the ChatServer.java file, we have:

```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    // Create final string using StringBuilder
    String stringBuilder = "";

    public String handleRequest(URI url) { 
        if (url.getPath().equals("/")) {
            return stringBuilder;
        } 
        // The request looks like this: add-message?s=<string>&user=<string>
        else if (url.getPath().contains("/add-message")) {
            // Two elements s=<string> and user=<string>
            String[] parameters = url.getQuery().split("&");
            // Separate s=<string>
            String[] sAndString = parameters[0].split("=");
            // Assign <string> to s
            String s = sAndString[1];
            // Separate user=<string>
            String[] userAndString = parameters[1].split("=");
            // Assign the <string> to user
            String user = userAndString[1];
            // Create String <user>: <message>
            String combinedString = user + "; " + s;

            stringBuilder = stringBuilder + combinedString + ("\n");            

            return stringBuilder;
        }
        else {
            return "404 Not Found!";
        }
    }
}


class ChatServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```
Next, in the Server.java file, we have:
```
// A simple web server using Java's built-in HttpServer
import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started!");
    }
}
```

Two screenshorts using the `/add-message`: \
![Image](RobertHelloLab2.JPG) \
In this screenshot, the `handleRequest()` method is called. \
The relevant argument for the `handleRequest()` method is a url. As seen in the image, the url path `/add-message?s=Hello&user=Robert` is used, and this is the argument for the method in this case. To keep track of the overall String to be returned, I use the class field `String stringBuilder = ""`. This keeps keep track of a single String that gets added to by incoming requests. \
The values of this field change with incoming requests that include `/add-message`. When requests that contain `/add-message` are recieved, the code in the if-statement for this condition run, and a new line is added to the initial stringBuilder. In this case, stringBuilder had gone from an empty String (`""`) to a String containing `"Robert: Hello"`, which is returned. 


![Image](AnnieHiLab2.JPG) \
 \
 \
In this screenshot, the `handleRequest()` method is once again called. \
Same as before, the relevant argument for the `handleRequest()` method is a url. As seen in the image, the url path `/add-message?s=Hi&user=Anne` is used, and this is the argument for the `handleRequest()` method in this case. Once again, to keep track of the overall String to be returned, I use the class field `String stringBuilder = "";`. Notice that `/add-message?s=Hello&user=Robert` had already been inputted into the url. This means the variable `stringBuilder` is currently set to be `"Robert: Hello\n`. Inputting the url `/add-message?s=Hi&user=Anne` adds to the initial String, and concatinates the `"Rober: Hello\n"` with `"Anne: Hello\n"`. We see the results of this in the screenshot above. \
 \
Also, note that to get the server running, the other methods are used, including the `main()` method, the `handle()` method, and the `start()` method. In the `main()` method (of `ChatServer`), the first command line argument (`args[0]`) is parsed as an integer and passed as the port number. \
In the terminal, we run the following to start the server:
```
javac Server.java
javac ChatServer.java
java ChatServer 4000
```
Notice that in this case, we used port number 4000. This port number is the argument for the `main()` method. 


## Part 2
Using the command line: \
![Image](labReport2AbsolutePath.JPG) \
As we can see from the image, the absolute path to the *private* key for my SSH key for logging into `ieng6` (on an EdStem workspace) is: `/home/.ssh/id_ed25519`. \
Aslo, as we can also see from the image, the absolute path to the *public* key for my SSH key for logging into `ieng6` (on an Edstem workspace) is: `/home/.ssh/id_ed25519.pub`. \
 \
Using the command line: \
![Image](labReport2PrivatePath.JPG) \
This screenshot depicts the *public* key that I copied to my account on `ieng6`. The absolute path on ieng6's file system is: `/home/linux/ieng6/oce/43/243/sstandlee/.ssh/authorized_keys`. \
 \
Below is a screenshot of a terminal interaction where I log into my `ieng6` account *without* being asked for a password: 
![Image](lab2LogInIeng6WithoutPassword.JPG) 


## Part 3
One of the key things I've learned that I didn't know before was how to remotely connect to a server. Specifically, we did this through the command `ssh myUsername@ieng6.ucsd.edu`, which initiates a secure connection to the server ieng6.ucsd.edu with my provided username. This secure connection allows me to access and manage files, execute commands, and perform tasks on the remote server. I also have know previous knowledge on building and running servers, so I learned that during Week 2 and Week 3 as well. 





