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



[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)