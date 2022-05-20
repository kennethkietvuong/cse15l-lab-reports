[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)

<meta http-equiv="refresh" content="10">

<body>
      <h1 style="text-align:center">Lab Report 4 - Week 8</h1>
      <h2 style="text-align:center">Clean Coding Practice</h2>
   </body>

Alrighty, hey guys! This is the fourth lab report for CSE 15L. There aren't any new concepts that are game-changing that will be discussed this time, but it's all about **refining** and **cleaning** up your code.

What does **cleaning up your code** mean? In short, it means to make your code ***more easy to read and understand***. In the efforts of making your code more better, it's not all about adding more safety measures to make sure your code works, but rather to make the code more *satisfying* and *appealing* to people who do want to *peruse* your code.

Simply, ***clean code is code that clearly displays its intended purpose and that is is simple.***

Below, I will test 3 snippets to another person's implementation of `MarkdownParse` with my own implementation:

* My [`MarkdownParse`](https://github.com/kennethkietvuong/markdown-parse-copy)

* Other's [`MarkdownParse`](https://github.com/ANGUYEN625/markdown-parser)

<p>&nbsp;</p>

## Snippet 1


```md
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

## Snippet 2
```md
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```

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

[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)