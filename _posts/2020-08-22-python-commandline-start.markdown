---
layout: post
title:  "Getting started with Python"
date:   2020-08-22 12:01:25 +0200
categories: jekyll update
---

## Introduction

Repetitive tasks are exhausting to us humans. To computers, they are a breeze. So why should we be the ones doing them? With a tiny bit of scripting, we can make them the job of our machines!

Enter Python, a programming language (named after Monty Python, not a snake). Beginner-friendly, readable and incredibly versatile. It allows you to automate and augment your workflows, letting you focus on the interesting parts.

In this post, I will show you how to install Python, use it – both from the default launcher and Windows' PowerShell – and customize some settings, making it easily accessible.

# Prerequisites

I assume:

**1. You have control over your computer**;  
   Seems obvious... but computers facing the general public, such as those in libraries, might have restricted access. Some options – e.g. installing Python – might not be available.

**2. Your operating system is Windows 10**;  
   The tutorial should also work on previous versions, but I can't promise it does. Even if you have an older version, you can still try and give me some feedback if anything goes wrong.

**3. You have Notepad, PowerShell and File Explorer**.  
   If 2. is true for you, than this should be as well, since Windows has all these programs installed by default. Of course, if you prefer other programs and feel familiar with them, you can use them instead.

## The basics

# 1. Installing Python

To get Python, visit [its website](www.python.org). It should automatically offer the Python version most suited for your operating system.

After you download it, you should have a `python-<x.y.z>.exe` file, where `<x.y.z>` will be your version number. Click on it to launch the installer.

Make sure the `tcl/tk and IDLE` option is selected on the first screen (IDLE is the editor we're going to use).

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/pyinstall1.jpg"> 

When you reach the second screen, make sure `Add Python to environment variables` is selected. This option will allow you to call Python from any folder.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/pyinstall2.jpg"> 

The rest is up to you, you can stick to the default options, although I **really** recommend choosing the *pip* option from the first screen as well.

{:.info}
If you have already installed Python without choosing the options I recommend, you can still click the *.exe* file again, select the `Modify...` option and choose them; no need to reinstall the whole thing.

Python is a *programming language*, which means that it's just a set of logical rules; it has no physical form of its own and has to be launched **inside another program**.

The launcher installed by default is called IDLE. It's simple but sweet. And specifically tailored to Python, so it *understands it* and can offer some helpful features (e.g. applying different text color to commands which have a special meaning in Python).

Let's try it out! You can open IDLE from the start menu, under the *Python* tab:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/python_in_startmenu.jpg"> 

You will see Python's **interactive shell**, a place where you can enter Python commands and see your results right away.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/python_hello.jpg"> 

Type in (or copy and paste after the `>>>`) the text below, then confirm by pressing `Enter`{:.kbd}.

```python
print('Hello!')
```

It will be displayed in blue and the `>>>` prompt will jump to the next line:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/python_hello2.jpg"> 

Meaning that your Python is working!

# 2. Creating your first script

Python's interactive mode is useful for poking around, but it doesn't store any commands between sessions. You usually want to prepare some functions beforehand, save them somewhere on your disk and then load them when you need them.

This is what *.py* files are used for. We will create and save our first Python script, using IDLE's editor mode.

{:.info}
Python's *.py* files are simple text files; if you wanted, you could create them in Notepad as well and save with the *.py* extension. We are only using IDLE's editor for convenience.

Without leaving IDLE, open the script editor (`Ctrl`{:.kbd}+`N`{:.kbd} or `File > New file`{:.win} from the top left menu). You will see an empty window similar to Notepad. This is where you can write Python files.

Let's write something to test our script, like:

```python
print('Hello from script!')
```
<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/hello_untitled.jpg"> 

Let's run the script. Press *F5*{:.kbd}. A prompt will appear asking you to save the file first:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/src_must_be_saved.jpg"> 

Choose OK to open the standard file saving window. I have created a new folder, `C:\MyScripts`, which I will also use as my future folder for Python scripts. If you want to follow the tutorial to the letter, do the same; you can also add any other name you want.

In the bottom field, enter the name you want to give to your Python file and confirm (I used `myscript`). You don't have to type in the *.py* extension, it will be added automatically.

IDLE's interactive mode will be launched and you should see your text, `Hello from script!`, printed in blue:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/hello_from_script_result.jpg"> 

If it works, it means that you can now write helpful scripts and place them in any folders you want!

The next step is to reach Python from anywhere, not just by opening its scripts. For this, we'll use the default utility bundled with Windows – PowerShell.

# 3. Python in PowerShell

Simply put: PowerShell is a minimalistic (text-only, no graphical gimmicks) tool for launching other programs. You can – and usually will – launch it from your File Explorer. Open it from the top menu, after clicking the dark-blue `File`{:.win} tab:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/powershell_open.jpg"> 

{:.info}
**Trick:**  
When you use the File Explorer, you can also hold the `Shift`{:.kbd} button and right-click anywhere with the mouse; you will see the `Open PowerShell here`{:.win} option in the popup menu, which is normally hidden.

Click the option to open PowerShell. It has this minimalistic look, like from all the mainstream hacker movies:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/powershell_first_launch.jpg"> 

Look at the prompt:
* The first two letters, `PS`, indicate that it's PowerShell.
* Then you have the currently active directory – the folder "you are currently in". It's `C:\Examples\Python_first_steps` in my case.

  In PowerShell, **active directory matters**. Alot. In Python's case, it usually matters when you *import* files, meaning that you load the code contained inside them. By default, you can only call your ad-hoc scripts from the same folder where you put them. 

* The last part is the `>` sign and a blinking cursor after it. This is where you can type commands; there are many of them available and they don't have to be related to Python at all!

Let's check if we can reach Python from anywhere. Type `python`{:.pshell} and confirm with `Enter`{:.kbd}. You should see the same familiar mode as in IDLE, but less colorful:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/powershell_python.jpg">

{:.info}
**Travel analogy**:  
Imagine Python is a travelling artist. Python has great potential, but in order to create anything, he/she has to get some personal space first. IDLE and PowerShell are two of many places which can host our traveller and provide this space.  
IDLE is like the house of Python's distant relative. The host knows Python well and adjusts decorations to our artist's preferences (*syntax highlighting*).  
PowerShell is like a large hotel. It can accept many different guests, so Python has to check in before getting a room (hence we have to type `python`{:.pshell}). It also does not cater to Python's specific tastes (*no highlighting*), but has some general useful facilities (like *history* and *autocompletion*, not discussed here).


Let's stop for a bit and imagine the potential. What if, in the future, we could just move to a folder with the files we need to translate, open PowerShell, type `python do_my_job`{:.pshell} and see all boring parts done before our eyes? Just enough to aid us without making us redundant of course ;)

This future might not be that far, but we have to lay some more foundation and customize our settings a bit. Don't close PowerShell yet!

## Customizations

# 4. Locating Python's source folder

We will be playing around with some of Python's settings now. To do it, we should get to its core folder, buried deep within the files. There are many ways to find it... but since we have Python open in PowerShell, we might as well use it to show us the path.

First, with Python still active in PowerShell, type (or copy from here):

`import sys`{:.pshell}

Confirm by pressing `Enter`{:.kbd}. You should receive no visual feedback – apart from the console jumping to the next line – but trust me, all we needed has been loaded. Now type or copy:

`for p in sys.path: print(p)`{:.pshell}

Press `Enter`{:.kbd} **twice**. This is the result we should see (one of the paths highlighted by me; of course, your user name will also be different):

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/sys_path.jpg"> 

{:.info}
If you want to know what's happening: `sys.path` belongs to the `sys` module we've imported. It's a list of paths where Python searches for its scripts. By using `for...`, we move through its elements one by one. `p` is just a temporary name given to each of these elements. And we use `print`, because we want each path in a form we can easily copy. If we hadn't used it, we would e.g. have double slashes (`\\`) instead of single ones.

Copy the path ending with *lib*, which I've highlighted in the picture above. This is where Python stores its files.

Then open File Explorer and click on the right side of the address bar (marked in red):

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/file_selection_window.jpg"> 

This will select the whole path as text:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/file_selection_window2.jpg"> 

Paste the `...\lib` path you've copied from PowerShell:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/file_selection_window3.jpg"> 

...and confirm by pressing `Enter`{:.kbd}. You are now inside Python's main folder. This is what you should see:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/python_lib_dir.jpg"> 

I have marked two folders which are of interest to us. We will work on them during the next two steps, so don't close this Explorer window yet. I'll be referring to it as the **Python folder window**.

# 5. Making IDLE open *.py* files by default

By default, *.py* files get **launched** when you double-click them. Not much happens – you catch a glimpse of a dark console window when the code inside gets executed, then it disappears.

If you want to open a file for **editing**, you can right-click its name, select `Edit with IDLE`{:.win}, and then choose the option to the right:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/open_with_idle_option.jpg">

But right-clicking and selecting is rather slow. If (when!) we get addicted to Python, we will be editing files often, so let's make it as ergonomic as we can. Let's make IDLE open the file in edit mode after a double left click.

Right-click on any *.py* file, then select `Open with`{:.win}.  
You will see a list of programs which could be used to open the file. Unfortunately, IDLE is not on it. Click `More apps`{:.win} and also **the box next to the "Always use..." option**.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/open_with_menu.jpg"> 

IDLE's still not there. Scroll down to the end of the list and click the `Look for another app on this PC`{:.win} option. 

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/py_more_options.jpg"> 

A File Explorer window will appear, from which you can choose any file we want. I'll call it **IDLE selection window** for now. Don't close it, we'll get back to it.

Now we want the path to our IDLE, which is buried surprisingly deep in the files! To get it, open the **Python folder window** from before. There, copy the path from the upper bar (using the same steps as in the previous point).  
Move back to the **IDLE selection window** and click on the right side of the filepath bar, like before. Paste the path you copied and confirm. You will move to Python's main directory. Move to the `idlelib` folder, where IDLE is stored. There, you can select `idle.bat`:

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/file_selection_window4.jpg"> 

Confirm. The Python file you originally clicked should open in IDLE, ready for editing. Well done! From now on, you can open all *.py* files with a double left-click. Making quick changes to your scripts will be quick and smooth.

Here, I'd like to give credit to [this great answer from StackOverflow](https://stackoverflow.com/questions/24988880/set-python-idle-as-default-program-to-open-py-extensions), which showed me where to look for IDLE!

# 6. Creating a folder for your Python scripts

Currently, you can create your own scripts and launch Python from anywhere...  but how about calling **your own scripts from anywhere**? Let's create a separate folder for all the scripts we make ourselves. This way, we can easily launch them, organise them and move them between computers.

To do this, we have to create a separate folder and "let Python know" that it should also look inside it whenever we try to import files.

You can create this folder in any location. In my case, I used the `C:\\PyScripts` folder created in step 2. Inside it, I put a `myscript.py` file, which only contains `print('Hello from anywhere!')` and nothing else.

Remember the **Python folder window** from before, where I've marked two subfolders? One of them is `site_packages`. It's the place where Python looks for scripts to import. We can also put paths to our custom folders inside it!

Open this `site_packages` folder and create a new text file by e.g. right-clicking and selecting `New > Text Document`{:.win}. **The file can have any name, but must end with the .pth extension** ([source](https://stackoverflow.com/questions/3402168/permanently-add-a-directory-to-pythonpath)).

Then open the file with Notepad (right-click, `Open with...`{:.win}). Inside it, enter the path to the custom folder you've created.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/myscripts_pth_file.jpg"> 

Let's test it out! Using File Explorer, move to ANY location and open PowerShell. Inside it, type `python`{:.pshell} to enter the interactive mode. And then type `import x`{:.pshell}, putting the name of your file (without *.py*) instead of `x`. Confirm.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/hello_anywhere.jpg"> 

Look at the first line – it shows that I'm calling PowerShell from the `D:\` location. And yet, when I import a Python script called `myscript.py` located somewhere else (in `C:\MyScripts`), it still works!

{:.info}
If you wanted, you could also avoid creating your own folder and simply put your scripts in `site_packages` – they would still be accessible from anywhere. But as you download more Python packages, it's easy to forget which scripts are yours or, even worse, to accidentally overwrite them.

# 6b. Pinning your script folder in Explorer

If you want to go the extra mile (well, maybe more of a meter...), you can also add pin your Python folder to File Explorer's sidebar. To do this, simply right click on it in File Explorer and select `Pin to Quick access`{:.win}.

Now, as you move around the files in Explorer, it will always be visible to your left, one click away.

<img src="{{ site.baseurl }}/assets/blogpost3_python_first_steps/quickpin.jpg"> 

# 7. Python from everywhere, in one line

This is more of a demonstration than a customization. If you completed the previous step and importing works, you can open a new PowerShell window anywhere and type:

`python -m myscript`{:.pshell}

...replacing `myscript` with the name of the script you've imported before.

This little `-m` is a so-called **flag** which indicates that we want to launch a specific script instead of Python in general.

...And sure enough, when we confirm, it does print our "Hello from anywhere". We can directly call all Python scripts from our custom folder this way. A single line is enough to reach Python from anywhere!

## Conclusion

After this tutorial, you:

* have a working version of Python on your computer;
* can launch Python from any folder on your computer, using PowerShell;
* can create and save Python scripts for further use;
* have a folder where you can place all your Python scripts to make them accessible from anywhere.

Here are some example workflows now available to you:

* Creating a single-use script:

  When you want a one-time "fire and forget" script to prepare a single set of files, you can quickly make a new one, refine it, launch it... And then leave it alone.

* Using custom scripts regularly

  Sometimes you find out that your jobs involve repeating steps and you come to the decision to "promote" some of your scripts to regular ones. In this case, you can just copy them to your custom folder and `import` their contents from anywhere, to use it in future situations.

* Making changes to existing scripts

  You can swiftly edit your scripts by double-clicking them and making changes in IDLE.

* Migrating to a new computer

  When you are moving to a different machine and want to keep your collection of Python scripts, you can just copy your custom folder, move it, and then, on your new machine, create a *.pth* file pointing to its path. With all scripts in one place, you don't risk forgetting anything.

Remember how I day-dreamt in point 3 about calling Python to do a large part of our jobs? Turns out we can't solve everything by typing `python do_my_job`{:.pshell}... It's actually `python -m do_my_job`{:.pshell} ;) 

In future posts, I will share some ideas for what this mythical `do_my_job` could be – I will review some example scripts and show when they could be useful. Stay tuned!
