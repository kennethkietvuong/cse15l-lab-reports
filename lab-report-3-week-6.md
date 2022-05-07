[back to main page](https://kennethkietvuong.github.io/cse15l-lab-reports/)

<meta http-equiv="refresh" content="10">

<body>
      <h1 style="text-align:center">Lab Report 3 - Week 6</h1>
      <h2 style="text-align:center">Continuous Integration &  More Unix</h2>
   </body>

Heyo! This is the third lab report for CSE 15L. This time around, we are now using the application of ***continuous integration*** with the addition of making our remote server access even *more* convenient.

***Continous integration*** is the application to the consistent upload of some sort of program/software and then goes through an automated test to check whether or not the overall program/software will be good for release.

For the most part of this lab report, I am going to be focusing on accessing GitHub and our remote server more conveniently. *Just think of it like you are in the carpool lane with no traffic compared to other normal lanes*.
<p>&nbsp;</p>

## Streamlining `ssh` Configuration
Usually, when we log into the remote server (`ieng6`), we type something along the lines of :

> `ssh cs15lsp22###@ieng6.ucsd.edu`

* After this, since we already have an SSH key, we will automatically log in

But the only thing that *may be a hassle* would be to **remember your account** (*which even I don't have it down*), so it would be preferable to have some sort of ***shortcut*** instead of copy & pasting your account from somewhere.

### The Solution
The easiest way to make this easier on ourselves is to make a key term that replaces our account. So, here's how:

1. Locate where you created your `ssh-keys` on your computer:
    > `~/.ssh/config`

    * *Should be within the `.ssh` folder*

2. Make a config file that tells `ssh` what username & nickname to use to log in to specific servers in `~/.ssh/config`.

![Image](/lab-report-assets/report3/config_where.png)
* Make sure that the config file has **no extensions**, where it it is **only a File** (ex. not a text file).

3. Open the config file through **any text editing program** (in my case, VSCode), and copy & paste this into it...then save!

    ```
    Host ieng6
        HostName ieng6.ucsd.edu
        User cs15lsp22###
    ```
    * For your user, it's just the front info before the @.

Now that we have the config file inside our `.ssh` folder, we can test if it worked or not through our terminal...and success!

![Image](/lab-report-assets/report3/using_ssh_shortcut.png)

Testing it further, let's try to use `scp` using our shortcut:

1. We can copy any file, so in this case, I made a file called [`testing.txt`](/lab-report-assets/report3/testing.txt)

2. Make sure you know where your file is located and then:

    > `scp testing.txt ieng6:~`
    * In my case, I had to find the directory of where my text file was (*ex. /randomfolder/testing.txt*)

![Image](/lab-report-assets/report3/scp_ssh_shortcut.png)

## GitHub Access via `ieng6`
Normally when we are in `ieng6`, we can *`clone`*, *`pull`*, and *`git status`* for our particular GitHub repository. Though we didn't see much **`commit` nor `push`** through the command line.

Apprently, when you try to commit or push, you'll likely run into this error:



![Image](/lab-report-assets/report3/remote_commit_fail1.png)
![Image](/lab-report-assets/report3/remote_commit_fail2.png)
* In my case, I tried to add a new file into my repository called `SkillDemo1` and commit that through `ieng6`.
* The error is that you cannot use a password and that you need to use some sort of token (similar to `ssh-keys`).

# The Solution
To be honest, this took so much effort to figure out how to allow pushing and all of that of GitHub from `ieng6`. But here's how I did it:

1. Make a key for GitHub through `key-gen` command & place it into your `.ssh` folder
![Image](/lab-report-assets/report3/github_key_ssh.png)
    * In my case, I named it `id_rsa_github`.

2. Copy the content within your GitHub public key
    * You can use the terminal to copy it in, or open any text editor to open the file:
    > `id_rsa_github.pub`
3. Go back to [GitHub](https://github.com/), go to settings, then under the **`SSh and GPG keys`**, add your copy and paste your key there.

![Image](/lab-report-assets/report3/ssh_keygithub.png)
* There should be at least a key like above (*I have multiple keys as I had trouble getting it to work except for the last key that is green*)