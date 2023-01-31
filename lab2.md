In the past couple labs, we worked on creating web servers and debugging code. This lab report will cover my StringServer, some buggy code from lab 3, and what I've learned more generally from CSE15L so far. 

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
When I run this on my own computer using `java StringServer 4000`, this code makes it such that:
- when I visit [http://localhost:4000/](http://localhost:4000/), the page displays a list of strings that are in the instance variable `list`
- when I visit [http://localhost:4000/add-message?s=string](http://localhost:4000/add-message?s=string) adds string to the end of `list`, and the page displays a list of strings that are in the instance variable `list`
- when I visit [http://localhost:4000/anything-else](http://localhost:4000/anything-else), the page displays `404 Not Found`

When I first open up the webpage, this is what it looks like. 

<img width="508" alt="image" src="https://user-images.githubusercontent.com/122497388/215607804-a9a1a9db-243b-439f-aa4f-ee7da6ff7f41.png">

In this screenshot, `handleRequest(http://localhost:4000/)` is called. No fields are changed by this request, and the webpage doesn't display anything because `list` does not have any elements at this time. 

Then, if I visit [http://localhost:4000/add-message?s=Hello](http://localhost:4000/add-message?s=Hello), this is what the page looks like.

<img width="475" alt="image" src="https://user-images.githubusercontent.com/122497388/215607244-e02f8a46-416e-4570-aca6-e3c70a018cea.png">

In this screenshot, `handleRequest(http://localhost:4000/add-message?s=Hello)` is called. "Hello" is appended to `list` as a result. The webpage now displays "Hello" because `list` only has the element "Hello". 

Finally, I visited [http://localhost:4000/add-message?s=How are you](http://localhost:4000/add-message?s=How%are%you), and this is what the page looked like.

<img width="588" alt="image" src="https://user-images.githubusercontent.com/122497388/215607486-15bd514a-2146-40ac-ae7e-95943c36eb33.png">

In this screenshot, `handleRequest(http://localhost:4000/add-message?s=How are you)` is called, so "How are you" is appended to `list`. The webpage now displays "Hello" and "How are you" because `list` now has two elements: "Hello" and "How are you". 

## Part 2: Lab 3 Bugs

 In Lab 3, we were given some buggy code at [https://github.com/ucsd-cse15l-w23/lab3](https://github.com/ucsd-cse15l-w23/lab3). My favorite was the method  `static int[] reversed(int[] arr)` in [ArrayExamples.java](https://github.com/ucsd-cse15l-w23/lab3/blob/main/ArrayExamples.java). 
 
 ```
  static int[] reversed(int[] arr) {
    int[] newArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = newArray[arr.length - i - 1];
    }
    return arr;
  }
 ```
 
 At first glance, it seems to approach the problem exactly as I would. It initializes a `newArray` of the same length, iterates through `arr`, and makes sure the item at `newArray[arr.length-i-1]` is the same as `arr[i]`. 
 However, the first red flag is seemingly that it returns `arr`, not `newArray`, so it'd return the non-reversed array, even if `newArray` was the perfect reversed array.
 Moreover, I realized in the for loop, `arr` is on the left side of the assignment operator (=). Therefore, what happens is that `newArray` is set to an array of 0s as a default value, so `arr` is set to an array of 0s, and `arr` is returned. Thus, regardless of what `arr` is given, an array of all 0s is returned. 
 
 A non-failure inducing input was given in [ArrayTests.java](https://github.com/ucsd-cse15l-w23/lab3/blob/main/ArrayTests.java): `ArrayExamples.reversed(new int[]{ })`.Since there are no elements, the for loop doesn't run, and the original array is returned. Since the array is empty, it's palindromic, and the original array is the reversed array.
 
 A failure inducing input would be `ArrayExamples.reversed(new int[]{1, 2, 3, 4})`. It would return '{0, 0, 0, 0}', not '{4,3,2,1}'.

## Part 3: What I Learned

I learned how to host things on localhost using URLHandler with a port number. Priorly, I knew HTML and JavaScript, but had no way of seeing cumulative results for my programming like I can see in java. I will revisit my JavaScript notes and google how to get similar results from a prettier User Interface, using JavaScript tools instead of `System.out.print()`.
