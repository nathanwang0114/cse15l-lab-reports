# Week 2 Lab Report
---
## Part 1: Writing a Web Server Called String Server
**Code for StringerServer**
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
    String word = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                if(word.equals("")) {
                    word += parameters[1];
                }
                else {
                    word = word + "\n" + parameters[1];
                }
                return word;
            }
        }
        return "404 Not Found!";
    }
}

class StringServer {
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
**Screenshots of `add/message` being used**
