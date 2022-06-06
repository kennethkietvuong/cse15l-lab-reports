[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)

<meta http-equiv="refresh" content="10">

<body>
      <h1 style="text-align:center">Lab Report 5 - Week 10</h1>
      <h2 style="text-align:center">More Debugging w/ Large Code Bases</h2>
   </body>

Yoooooo, this is the fifth and final lab report for CSE 15L! There isn't nothing special this time around about debugging, but it's more about the specifics of debugging and making it more *versatile*. 

Within debugging, there's a lot more useful things to make testing your code more convenient. In this case, we could use ***scripts*** and using ***vim*** to have more control to our code & tests.

<p>&nbsp;</p>

## Using `vimdiff`

If we have two separate programs which do the same function, how do we compare the results when we are dealing with a *huuuuge* amount of tests & files? Surely you aren't going to look at each file one by one...? That's going to take forever, so to compare how two programs' results of the same function, we can use a `vim` command!

The command I used to find the different results of two `MarkdownParse` programs (*mine & lab 9's*) is `vimdiff`, where I compared two text files with one and another to see if the results match or are different!

* My [`results.txt`](/lab-report-assets/report5/results_mine.txt)

* Lab 9's [`results.txt`](/lab-report-assets/report5/results_lab9.txt)

The specific command I used for `vimdiff` is:
> `vimdiff my-markdown-parser/results.txt markdown-parser-lab9/results.txt`

* The first `results.txt` is comparing a file within my markdown directory
* The second `results.txt` is comparing a file within lab 9's markdown directory

<p>&nbsp;</p>

### Test 421
For the test case #421, using `vimdiff`, here are the results:

![Image](/lab-report-assets/report5/test-file421.png)

* *The left is my markdown & the right is lab 9's markdown (open the image in a new tab to see better!)*
   * My markdown resulted in `[]`
   * Lab 9's markdown resulted in `[/url]`

The test file for #421 is:
```md
**foo [bar](/url)**
```

* Looking at the link, it looks like the output should result in `[/url]`

   * It looks like ***lab 9's implementation of a markdown parser was <u>correct</u>***
   * While ***my markdown parser was <u>not successful</u>***

So what was wrong with my implementation?
* I think the core *bug* with my implementation is that my `MarkdownParse` looks for **actual and real valid link** that would work <u>realistically</u>. So when it parsed through the test file of #421, it saw `/url` as a link, ***but not a valid link***. If I were to fix my Markdown, I would probably deal with the *code that checks actual valid links*.

![Image](/lab-report-assets/report5/code_debug.png)

<p>&nbsp;</p>

### Test 194
For test case #194, using `vimdiff`, the results are:

![Image](/lab-report-assets/report5/test-file194.png)

* *The left is my markdown & the right is lab 9's markdown (open the image in a new tab to see better!)*
   * My markdown resulted in `[]`
   * Lab 9's markdown resulted in `[url]`

The test file for #194 is:
```md
[Foo*bar\]]:my_(url) 'title (with parens)'

[Foo*bar\]]
```

* Just looking at this file, it clearly looks like the output should result in `[]`

   * Thus, I can conclude that ***lab 9's implementation was <u>wrong</u>***
   * While ***my markdown parser was <u>right</u>***

So what went wrong compared to my markdown and lab 9's markdown implementation?
* I believe that the **bug** that overall came about with lab 9's is that they didn't acknowledge the **overlapping syntaxes** that would consider the link to be invalid. In the markdown preview, it does show that it works, but just looking at the test file, it clearly should not work if there are a ton of weird syntaxes that counteract the syntax for a link. I'm not sure about a fix for lab 9's markdown, but a suggestion would be to **check the overlapping syntax formatting issues first** before checking the actual link.

![Image](/lab-report-assets/report5/code-debug-lab9.png)


## Conclusion
To sum it up, ***there is no perfect `MarkdownParse`***, where each one has its advantages than others (*includes weaknesses & flaws*). For the most part, my `MarkdownParse` had a huge difference than lab 9's `MarkdownParse` due to my code checking if it is an actual & real valid link, while lab 9 does not check for syntax issues. Either way, ***if it works, it works***.

*Shoutout to the amazing TAs & the Prof himself for making the course interesting and neat! While sometimes I felt that some weeks were a hassle, I overall enjoyed the course. Until next time folks!*

[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)