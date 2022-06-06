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

### Test 421
For the test case #421, using `vimdiff`, here are the results:

![Image](/lab-report-assets/report5/test-file421.png)

* *The left is my markdown & the right is lab 9's markdown*
   * My markdown resulted in `[]`
   * Lab 9's markdown resulted in `[/url]`

The test file for #421 is:
```md
**foo [bar](/url)**
```

* Looking at the link, it looks like the output should result in `[/url]`

   * It looks like ***lab 9's implementation of a markdown parser was correct***
   * While my markdown parser was ***not successful***

So what was wrong with my implementation?
* I think the core *bug* with my implementation is that my `MarkdownParse` looks for **actual and real valid link** that would work <u>realistically</u>. So when it parsed through the test file of #421, it saw `/url` as a link, ***but not a valid link***. If I were to fix my Markdown, I would probably deal with the *code that checks actual valid links*.

![Image](/lab-report-assets/report5/code_debug.png)



[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)