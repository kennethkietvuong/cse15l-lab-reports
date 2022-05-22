[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)

<meta http-equiv="refresh" content="10">

<body>
      <h1 style="text-align:center">Lab Report 4 - Week 8</h1>
      <h2 style="text-align:center">Clean Coding Practice</h2>
   </body>

Alrighty, hey guys! This is the fourth lab report for CSE 15L. There aren't any new concepts that are game-changing that will be discussed this time, but it's all about **refining** and **cleaning** up your code.

What does **cleaning up your code** mean? In short, it means to make your code ***more easy to read and understand***. In the efforts of making your code more better, it's not all about adding more safety measures to make sure your code works, but rather to make the code more *satisfying* and *appealing* to people who do want to *peruse* your code.

Simply, ***clean code is code that clearly displays its intended purpose and that is is simple.***

Below, I will test 3 snippets to another person's implementation of `MarkdownParse` with my own implementation. These snippets deal with the **markdown syntax** when using *backticks*.

* My [`MarkdownParse`](https://github.com/JasonMorris1/markdown-parser)

* Other's [`MarkdownParse`](https://github.com/ANGUYEN625/markdown-parser)

<p>&nbsp;</p>

## Snippet 1
```md
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

The first snippet here shows a clear issue with using the backticks syntax within a link format. In this case, when running `MarkdownParse.java`, it should produce a list of:
> `["google.com"]`

Everything else (*besides the third line*) in the snippet above clearly violates the markdown syntax for a link.

### Testing the Snippet
```java
    @Test
    public void snippet1() {
        List<String> expect = List.of("google.com");
        try {
            ArrayList<String> links = MarkdownParse.getLinks(readFile("snippet1.md"));
            assertEquals(links, expect);
        }
        catch (IOException e) {
            e.printStackTrace();
        }
    }
```
Within `MarkdownParseTest.java`, here is the code that I will be using to see whether or not my implementation and someone else's implementation will work.
* Note: I put the snippet into a file called `snippet1.md`

### My Implementation
After running the file to my implementation, it seems like my `MarkdownParse` **didn't work** as expected:

![Image](/lab-report-assets/report4/snippet1_own_fail.png)

### Other Implementation
After running the file to someone else's implementation, it also **failed**:

![Image](/lab-report-assets/report4/snippet1_other_fail.png)
* Note: *Besides the snippet failed test, this implementation had other issues also!*

### Clean Code Change
Overall, if I had to improve on the code by adding a **small code change** (*as per clean code guidelines*), I think it <u>may likely be possible</u> to deal with the backtick syntax issues with markdown. For example:
* Could add a few lines dealing with the backticks itself, so before checking where the parentheses and brackets are, first check the backticks are within the link format itself.
    * Similar to how we locate the URL of the link within the parenthese, we locate what's in-between the backticks to see if there are parenthese & brackets (*so we can not consider it to be a valid link and move on*).

## Snippet 2
```md
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```

For the second snippet, it deals with nested formatting potential issues with markdown. In this case, when running `MarkdownParse.java`, it should produce a list of:
> `[]`

*If it doesn't look like an obvious valid link, it's not a valid link.*

### Testing the Snippet
```java
    @Test
    public void snippet2() {
        List<String> expect = List.of();
        try {
            ArrayList<String> links = MarkdownParse.getLinks(readFile("snippet2.md"));
            assertEquals(links, expect);
        }
        catch (IOException e) {
            e.printStackTrace();
        }
    }
```
Within `MarkdownParseTest.java`, above is the next test for snippet 2.
* Note: I put the snippet into a file called `snippet2.md`

### My Implementation
After running the tester, it looks like it **passed**!

![Image](/lab-report-assets/report4/snippet2_own_pass.png)
* Note: *Snippet 1 still remains as an issue.*

### Other Implementation
After running on someone else's implementation, their tests for `MarkdownParse.java` seems to have **failed**!

![Image](/lab-report-assets/report4/snippet2_other_fail.png)
* Note: *This implementation has additional issues*.

### Clean Code Change
So, how would I ***clean up my code*** with a small change? To be honest, my implementation passed so it's good enough. But, if I had to, one minor tweak would be to <u>make the code more simple or to make it look not as cluttered</u>. Besides that, any other changes would focus on the brackets and the parentheses when dealing with nested stuff.
* Make the code look neat/organized
* Focus on adding on having a check to see if the actual URL link is valid in a real-world scenario.

## Snippet 3
```md
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```

For the third and last snippet, this deals with a ton of spaces where the parentheses/brackets are in different line. When we run `MarkdownParse.java`, it should produce a list of:
> `["https://www.twitter.com", "https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"]`

*The link format should have adjacent syntax that doesn't have empty spacing.*

### Testing the Snippet
```java
    @Test
    public void snippet3() {
        List<String> expect = List.of("https://www.twitter.com", "https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule");
        try {
            ArrayList<String> links = MarkdownParse.getLinks(readFile("snippet3.md"));
            assertEquals(links, expect);
        }
        catch (IOException e) {
            e.printStackTrace();
        }
    }
```

Above is the snippet 3 test that I'll be using to check if the outputs match for `MarkdownParse.java`.
* Note: I put the snippet into a file called `snippet3.md`

### My Implementation
After running the tester, it looks like it **passed** too!

![Image](/lab-report-assets/report4/snippet3_own_pass.png)
* Note: *Snippet 1 still remains as an issue.*

### Other Implementation
After running on someone else's implementation, their tests for `MarkdownParse.java` seems to have **failed** by a *huuuuge* margin:

![Image](/lab-report-assets/report4/snippet3_other_fail.png)
* Note: *This implementation has additional issues*.

### Clean Code Change
In making a **small code change** in my implementation for the basis of ***clean code***, I think it's good enough. There doesn't seem to be much to change, unless we want the empty spaces within a file to be considered also. My implementation focuses on links that are formatted next to each other. As long as they are within the next line of each other, it's okay. But if there's an empty white space in-between, that doesn't count as a valid link. Besides that it <u>may be possible to shorten or add some code to make it more better</u>.
* Add a few lines in considering white space in a text file as a condition or check for valid link
* Configure it so specific links are only valid
    * *Checking to see if a link looks like it works on a browser*

<p>&nbsp;</p>

[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)