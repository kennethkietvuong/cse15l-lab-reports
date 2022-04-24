[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)

<meta http-equiv="refresh" content="10">

<body>
      <h1 style="text-align:center">Lab Report 2 - Week 4</h1>
      <h2 style="text-align:center">Incremental Development & Debugging</h2>
   </body>

Hey y'all! This is the second lab report for CSE 15L. This is all about the concept and uses of ***incremental development*** with the addition of ***debugging***.

The main focus in incremental development is to do things *"one step at a time"*, where you would make a few changes and review those changes (*aka debugging*) before moving on to the next task or thing you will do.

This way, you won't have to worry about destroying or messing up your entire program in one go.

<p>&nbsp;</p>

## The Program

The program that we will be incrementally developing to be better will be called `MarkdownParse`. Essentially, the main purpose of the program is to parse through files (such as text files) and record all given valid URLs (links) into a list.

Below is the original code to `MarkdownParse.java` without any changes and tests.

```java
//https://howtodoinjava.com/java/io/java-read-file-to-string-examples/

import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.util.ArrayList;

public class MarkdownParse {

    public static ArrayList<String> getLinks(String markdown) {
        ArrayList<String> toReturn = new ArrayList<>();
        // find the next [, then find the ], then find the (, then read link upto next )
        int currentIndex = 0;
        while(currentIndex < markdown.length()) {
            int openBracket = markdown.indexOf("[", currentIndex);
            int closeBracket = markdown.indexOf("]", openBracket);
            int openParen = markdown.indexOf("(", closeBracket);
            int closeParen = markdown.indexOf(")", openParen);
            toReturn.add(markdown.substring(openParen + 1, closeParen));
            currentIndex = closeParen + 1;
        }

        return toReturn;
    }


    public static void main(String[] args) throws IOException {
        Path fileName = Path.of(args[0]);
        String content = Files.readString(fileName);
        ArrayList<String> links = getLinks(content);
	    System.out.println(links);
    }
}
```

* In simple terms, the code reads the first opened and closed bracket in defining the string to be split into substrings, where the content inside the first opened and closed parentheses will considered a URL to be added into the list.

<p>&nbsp;</p>

## Improving the Program
So, with the original program, it looks good enough *normally*. Though this poses a problem if there were cases where links aren't read or that an invalid link is included.

This is where we use test cases to put our program to the test if it needs to be more *refined*.

---

### Test 1 - Empty Line At End of Text File
Before I tried any tests, I initally ran `MarkdownParse` with the given test file [`test-file.md`](/lab-report-assets/report2/test-file.md).

After compiling and running the program with the given test file, my terminal **froze**! About half a minute later, I received an ***out of memory error***.

![Image](/lab-report-assets/report2/lab-report-2-images/test1_nomemory_symptom.png)

* Whenever we get an unintended output, we consider that as a **symptom**. In this case here with the given text file `test-file.md`, there's something about its input that makes `MarkdownParse` *not work*.

So, now that we have a symptom, we have to figure out what is wrong with our program. After some time, here is the solution:

![Image](/lab-report-assets/report2/lab-report-2-images/test1_fix.png)

Now when we run the program, we now get:

![Image](/lab-report-assets/report2/lab-report-2-images/test1_output.png)

Our expected output matches with the actual output now...hooray! But what was the problem to begin with?
1. First off, let's focus on the **failure-inducing input** (or our test file that made our program not work).
    ```md
    # Title

    [link1](https://something.com)
    [link2](some-thing.html)

    ```
    * The issue that caused `MarkdownParse` to work work occurred at the end, where there was an ***empty line space after the last link***.
2. This implies that the **bug** with our program is that it ***continues to parse through the file even though it has reached the end***.
3. Thus the **symptom occurs**, where the run-time stacks up to the point my computer ran out of memory for it to continue on!

---

### Test 2 - Bracket with No Parentheses
One test that I did was to try a given link title but with no actual link at all. Here is the text file here: [`test2.md`](/lab-report-assets/report2/test2.md).

I found that as long as there is brackets and parentheses, the program works as intended. But what if there were **no parentheses** at all (*vice-versa with brackets too*)?

Similarly like Test 1, I eventually recevied an ***out of memory error***.

![Image](/lab-report-assets/report2/lab-report-2-images/test2_nomemory_symptom.png)

* Again, this is the **symptom** to our program of `MarkdownParse`.

Instead of just singling out that one symptom of the no parentheses. My partner and I further resolved the other cases where there were no brackets and extra variations between brackets and parentheses:

![Image](/lab-report-assets/report2/lab-report-2-images/test2_fix.png)

When we run the program, we get the expected:

![Image](/lab-report-assets/report2/lab-report-2-images/test2_output.png)

1. Let's go into depth about the **failure-inducing input**:
    ```md
    My favorite search engine is [Duck Duck Go]() TEST

    My favorite search engine is [second](gadgadsgadsg)
    My favorite search engine is [first]
    ```
    * Basically the initial program ***reads whenever the next bracket or parentheses opens and closes***. Between that is considered a string of substrings that would make up the URL.
2. This leads to the **bug**, where `MarkdownParse` reads the next line(s) when it is not suppose to.
    * *The brackets and parentheses denote a start and end.*
3. Thus similarly like test 1, the **symptom occurs**, where the run-time goes over my computer's memory causing the out-of-memory error.

---

### Test 3 - "Invisible" Invalid Link Counts as Valid
insert text here