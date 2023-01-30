In the past couple labs, we worked on creating web servers and debugging code. This lab report will cover my StringServer, some failure-inducing input from lab 3, and what I've learned more generally from CSE15L so far. 

## Part 1: StringServer.java

The goal of StringServer is to keep track of a single string that gets added to by incoming requests. 
I implemented it by first cloning the github repository for NumberServer from lab 2 that was provided to us on the class webpage: [https://github.com/ucsd-cse15l-f22/wavelet](https://github.com/ucsd-cse15l-f22/wavelet). I didn't alter the .gitignore, Server.java, and README.md files at all.
I immediately renamed the NumberServer.java file to StringServer.java, and renamed the class NumberServer to StringServer. I imported `java.util.ArrayList` and added an instance variable `private ArrayList<String> list` to keep track of all the strings added. I then wrote a new default constructor for Handler to initialize `list`. 
Finally, I changed `public String handleRequest(URI url)` to account for the new behavior defined in the assignment. My full code for StringServer.java is provided below.

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    private ArrayList<String> list;

    public Handler(){
        this.list = new ArrayList<>();
    }

    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            String res = "";
            for(String str: this.list){
                res+= str + " \n";
            }
            return res;
        } else if (url.getPath().contains("/add-message")) {
            try {
                String[] parameters = url.getQuery().split("=");
                if(!parameters[0].equals("s")){
                    throw new Exception();
                } else {
                    this.list.add(parameters[1]);
                    String res = "";
                    for(String str: this.list){
                        res+= str + " \n";
                    }
                    return res;
                }
            } catch(Exception e) {
                return "404 Not Found!";
            }
        } else {
            return "404 Not Found!";
        }
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
<img width="427" alt="image" src="https://user-images.githubusercontent.com/122497388/215372612-0e178462-5d30-438d-ba48-5e64e70d1277.png">
<img width="543" alt="image" src="https://user-images.githubusercontent.com/122497388/215372737-9532b453-3209-4260-8596-fa484edb02e8.png">

## Part 2: Lab 3 Bugs

 

## Part 3: What I Learned
