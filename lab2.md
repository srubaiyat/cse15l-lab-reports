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

Then, if I visit [http://localhost:4000/add-message?s=Hello](http://localhost:4000/add-message?s=Hello), "Hello" is added to `list`, and this is what the page looks like.

<img width="400" alt="image" src="https://user-images.githubusercontent.com/122497388/215372612-0e178462-5d30-438d-ba48-5e64e70d1277.png">

Then, I can visit [http://localhost:4000/add-message?s=How are you](http://localhost:4000/add-message?s=How%are%you) to add another string "How are you" is added to `list`, and this is what the page looks like.

<img width="500" alt="image" src="https://user-images.githubusercontent.com/122497388/215372737-9532b453-3209-4260-8596-fa484edb02e8.png">

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
 
 A failure inducing input would be `ArrayExamples.reversed(new int[]{1, 2, 3, 4})`. It would return `{0, 0, 0, 0}', not '{4,3,2,1}'.

## Part 3: What I Learned
