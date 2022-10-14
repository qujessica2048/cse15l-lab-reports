# week 2 & 3 lab report!

## Part 1: Simplest Search Engine

A basic search engine that takes commands from the url. Specifically, this search engine takes word inputs, adds them to a list, and then allows the user to get a list of words that contains the queried word.
&nbsp;

For example, some commands would be:
```
/add?s=anewstringtoadd

/add?s=pineapple

/add?s=apple

/search?s=app
(would return pineapple and apple)
```

&nbsp;

### 1.1 Implementation

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {

    ArrayList<String> words = new ArrayList<>();

    @Override
    public String handleRequest(URI url) {
        
        if (url.getPath().contains("/add")) {
            String[] parameters = url.getQuery().split("=");
            if (parameters[0].equals("s")) {
                if (!words.contains(parameters[1])) {
                    words.add(parameters[1]);
                }
                return String.format(parameters[1] + " added!");
            }
        } else if (url.getPath().contains("/search")) {
            String[] parameters = url.getQuery().split("=");
            ArrayList<String> searched = new ArrayList<>();
            for (String word : words) {
                if (word.contains(parameters[1])) {
                    searched.add(word);
                }
            }
            return searched.toString();
        } else {
            return "hi";
        }
        return "404 Not Found!";
    }
}

class SearchEngine {
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
&nbsp;

### 1.2 Loading
Opening the website -- here, the classes in ```Server.java``` are run to create the server. ```SearchEngine.java``` takes in a port number when it is run, which allows it to create a new ```Server```. In this instance, the port number ```4000``` was used.

![Image](res\lab3\start.png)
&nbsp;

### 1.3 ```/add?s=```
Adding words to a word bank -- here, the method ```handleRequest``` in ```NumberServer.java``` is run, which parses the URL for keywords. In the next 3 screenshots, this is shown by the ```/add?s=``` followed by some word, and this is passed to the ```handleRequest``` method in ```SearchEngine.java```, which adds the word to a word bank ( ```ArrayList<String> words``` ).

![Image](res\lab3\jack.png)

At this point, ```words``` contains ```["jack"]```.

![Image](res\lab3\jill.png)

At this point, ```words``` contains ```["jack", "jill"]```.

![Image](res\lab3\jordan.png)

At this point, ```words``` contains ```["jack", "jill", "jordan"]```.

![Image](res\lab3\jarame.png)

At this point, ```words``` contains ```["jack", "jill", "jordan", "jarame"]```.

&nbsp;

### 1.4 ```/search?q=```
Searching in the word bank the keyword is now ```search```, but the method doing this in ```SearchEngine.java``` is still ```handleRequest```.
&nbsp;

If a search is put in for ```"j"```, the site should show a list of all the words that include ```"j"``` like so:

![Image](res\lab3\searchJ.png)
&nbsp;

If a search is put in, instead for ```"ja"```, all the words containing ```"ja"``` should show up like so:

![Image](res\lab3\searchJa.png)

&nbsp;

## Part 2: Bugs
who doesn't love bugs :(

|File & Method     | Failure-inducing Input    | Symptom       | Bug       | Connection  |
| :---        | :---        |         :---    |         :---    | :---  |
| ```averageWithoutLowest(double[] arr)``` from ```ArrayExamples.java```     | Input with the lowest number occurring > 1 time: ```{1.0, 2.0, 1.0, 3.0, 4.0}```      |   ```java.lang.AssertionError: expected:[2.5] but was:[2.25]```   |    Mistakenly skips all numbers that are equal to the lowest when it should only skip one. To fix, subtract the lowest number from the total sum once and then divide. | Since the method skipped **all** occurences of the lowest number, it skipped ```1.0``` twice when calculating the sum and got ```9.0/4 = 2.25``` instead of ```10.0/4 = 2.5```.|
| ```filter(List<String> list, StringCheckerStartsWithA sc)``` from ```ListExamples.java```   | Input with length > 1: ```{"bob", "apple", "Amy"}```        |  ```java.lang.AssertionError: expected:[[apple, Amy]] but was:[[Amy, apple]```     |       Chosen elements were added to the front of the result array instead of the end. To fix, replace ```result.add(0, s);``` with ```result.add(s);```.  | The method was supposed to keep the items in the same order that they appeared in the input list, but adding the chosen items to the front of the result array reverses the order.    |

&nbsp;



