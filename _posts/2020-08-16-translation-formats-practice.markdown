---
layout: post
title:  "File formats in CAT tools 2 – direct editing"
date:   2020-08-16 13:50:25 +0200
categories: jekyll update
---

*This is a series of blog posts on file formats used by CAT (Computer-assisted translation) programs for storing translation data. Their aim is to share some knowledge which should allow us to tame our CAT tools better. Or to become independent from their whims.*

*This post discusses ways of editing file types often used by translators – XML files and archives – without actually using a CAT tool. If you want to learn about these filetypes first, see [Part 1]({{ site.baseurl }}{% link _posts/2020-05-11-translation-formats-intro.markdown %}).*

## Introduction

In a perfect world, things are simple: you get a file (*translation package*) for translation, you open it with a specified CAT tool. It opens easily, you translate it and send it back.

However, there are many reasons you may want to stray from the path and work with the files on your own terms. Some examples:

* You want to use your preferred CAT tool, but it does not directly support the format of the translation package.

  ([Example 1](https://www.proz.com/forum/sdl_trados_support/211489-how_to_work_on_a_xlz_file.html), [example 2](https://www.proz.com/forum/sdl_trados_support/344630-using_lionbridge_files_in_trados_2015_ok_reverting_back_lionbridge_says_not_ok.html), [example 3](https://community.sdl.com/product-groups/translationproductivity/f/studio/6040/working-with-xyleme-xlz-packages) and perhaps many others...)
* You don't need the full content of translation packages and only want to get specific files (e.g. glossaries) out of them.
* You want to change the status of some segments before loading them into your CAT tool.

  E.g. they might have been accidentally locked, so you can't edit them, but you have to... Oh, and you don't have time to wait for the agency to send a new version!
* After you finish your work, you are asked for some light find-and-replace corrections.

  But you are still traumatised by the CAT tool you were forced to use, and you don't want to see it ever again...
* Countless other reasons!

No matter what reason you may have, **you should be free to work with files in the way which is most comfortable to you**. If CAT tools make you face obstacles, you can bend them to your will.

# Prerequisites

In order to play with translation files, you only need a few programs bundled with Windows by default:

- **File Explorer** (installed by default on all Windows versions; however, the one I use is bundled with Windows 10 and I don't know if older ones support zip files);
- a **text editor** for opening files (on Windows, you can use the default Notepad or the free [Notepad++](https://notepad-plus-plus.org/); larger office suites, such as LibreOffice or Microsoft Word, are also OK);
- (optional, but helpful) any **web browser**: Firefox, Brave, Edge, maybe even Chrome.

If you want, you can also use a CAT tool compatible with the translation package format to check if the edited package opens correctly.

If you want to follow my example, find and download **Idiom WorldServer** and then get the *.xlz* package it uses for its tutorial.  
**Sidenote:** I chose Idiom's file, because I had some trouble finding any other *.xlz* packages on the web (though I know that the format is rather popular). For the purpose of future posts, I will probably upload a minimal file of my own.


## Stage 1: Unpacking

For this example, I use a translation package in the form of a zipped archive – an *.xlz* file.

Fun fact: this format is used by the two clunkiest, most unpleasant CAT tools I have used in my life: Idiom WorldServer and Lionbridge's TMS. For this reason, cracking this filetype is a way for me to confront the ghosts of the past :D

A little bit of overview: .xlz files are actually archive files. They contain an *.xlf* file, which is based on XML and the one we directly translate; there can also be an *.skl* (skeleton) file describing the original structure, and other supplementary files, such as glossaries (also XML-based, usually with the *.tbx* extension).

{:.info}
If you want a primer on archives and XML files, check out [the previous post]({{ site.baseurl }}{% link _posts/2020-05-11-translation-formats-intro.markdown %}).

Now let's get to the action! First, place the copy of the file in some separate directory. I personally use `C://Examples` in this case.

We would like to extract the files from the zip archive. However, unless you have some specific software installed, our File Explorer does not recognize the *.xlz* extension as an archive and does not give us the option directly.

We could use a zip-handling program here, such as 7Zip, to forcefully extract the files (I normally do, so my icon for the *.xlz* filetype has a *7Z* on it).  
Luckily, we don't have to – default Windows tools can also help us, but we have to convince them that this mysterious file is actually a zip archive. How? By renaming it to *.zip*!

To rename the file, either:
* right-click on its name and select the *Rename* option from the popup menu, **or**
* left-click the name and choose the *Rename* option from the upper menu (under the *File* tab).

I have marked both options below, using red boxes:

<img src="{{ site.baseurl }}/assets/blogpost2/file_rename.jpg">

{:.info}
**The fast way:**  
You can also left-click the filename and press *F2*{:.kbd} to start renaming!  
Then, you can press **any** arrow key (to deselect the name) and then the *End*{:.kbd} key (to jump to the end, after the extension).

My personal trick here is that I don't *replace* the extension with *.zip*, but rather **add it** to the end, getting *.xlz.zip*. It's a bit faster for a keyboard-based workflow... And, if I have to take a break in the middle of my work, I don't have to remember what the original extension was – it just stays there in the name :p

Type the *.zip* extension and press *Enter*{:.kbd} to confirm. A warning prompt appears:

<img src="{{ site.baseurl }}/assets/blogpost2/file_rename_warning.jpg">

It sounds scary, but don't worry! Like I mentioned in the first blog post, changing the extension does not change the file contents themselves. Click `Yes` or press *Enter*{:.kbd} again.  
After renaming, the file icon should change to that of a zip archive.

And it's not the only thing that's changed! If you double-click on the zip file, you will see the files inside as if it were a normal folder. The only indication is the file path, which ends with *.zip*.  
Also take a look at the top menu. A new tab, *Compressed Folder Tools*, has appeared! To extract the files, do the following steps:

1. Left-click the *.zip* file (if you are not "inside" it);
2. click the *Compressed Folder Tools* tab;
3. and then the `Extract all` option on the right-hand side.

<img src="{{ site.baseurl }}/assets/blogpost2/zip_extraction_steps.jpg">

A dialog box will appear, asking us about the folder we want to extract the files to. 

<img src="{{ site.baseurl }}/assets/blogpost2/file_extraction_popup.jpg">

By default, the folder will have the same name as the zip archive, just without the *.zip* extension. In my case, since I had the `idiom_tutorial_copy.xlz.zip` file in `C://Examples`, the path offered to me by default is `C://Examples/idiom_tutorial_copy.xlz`.

Fine by me, let's use this path! Click `Yes` or press *Enter*{:.kbd}. We now have our original zip archive and a folder with its contents, right next to it:

<img src="{{ site.baseurl }}/assets/blogpost2/after_extraction.jpg">

(Interestingly, the folder has the *.xlz* extension, but the icon of a folder... and it acts like one as well! This is because the *file vs folder* distinction is contained in the metadata, and not influenced by any extensions).

If your only goal was to get some files out of the package, then you can just copy them out and finish right here :)

## Stage 2: Modifying

After the archive is unpacked, we have a bunch of XML files (*.xlf*, *.tbx* and plain *.xml*). And these are perfectly editable.

<img src="{{ site.baseurl }}/assets/blogpost2/unpacking_results.jpg">

When browsing popular discussion boards for translators, I've seen many different cases of people editing XML directly, such as:

* removing the *machine-translated* tag from Trados' *.sdlxliff* files;
* changing the languages codes within a translation memory file if the current ones are not recognized by the CAT tool (e.g. *EN* to *EN-GB*);
* anonymizing the file (removing personal data).

All the use-cases seem interesting, but perhaps the last one is the one we could all benefit from. Therefore, I will make it the focus of my example.

The file I want to edit is `eGate Project for DWB Tutorial_tasks.xlf`, because it contains the actual source-translation pairs. This is where translators' personal data can be stored.

Browsing the file with Notepad would be a pain, since it shows its contents as a single, huge, black-and-white block of text.  
A better text editor would be great here... this is why I recommend Notepad++ for Windows users. But you have to download it from the Internet. Isn't there something included on all PCs, which would allow us to view XML in a pleasant way?

Did I mention *the Internet*? Actually, almost all PCs have a tool whose job is to constantly parse HTML files, which are very similar to XML. Yep, these are **our web browsers**!

We can open the *.xlf* file with the browser (e.g by right-clicking the file, then selecting `Open with` and choosing a browser, Firefox in my case). We will see its structure in all its glory, with indendation and highlights!

Browsers have one weakness though – although they are good at **displaying** XML, they are by default not suitable for **editing** it. You could of course open the developer tools or download some extension... seems fun, but this is out of my league, and I also want to stick to the basics ;)

Instead, let's use both tools together, by using the browser for viewing and the Notepad for replacing text! Here, I have put them both side by side:

<img src="{{ site.baseurl }}/assets/blogpost2/notepad_browser_compare.jpg">

> By your powers combined...

While skimming the document in Firefox, I notice that some of the tags have attributes related to a company (`company-name="Idiom"`) and to a translator (`contact-name="Tom Translator"`). Let's say that we don't want them in the file.

So we click on the Notepad window, press *Ctrl*{:.kbd}+*H*{:.kbd} to get the replacement popup. We put:
* `Tom Translator` in the *Find* field;
* `Anonymous` (or any other name) in the *Replace* field.

<img src="{{ site.baseurl }}/assets/blogpost2/replace_window.jpg">

Then we click `Replace All`. All mentions of the translator should disappear. After we are done, we can save (*Ctrl*{:.kbd}+*S*{:.kbd}) the file.

**Warning:**  
The replacements were safe in this case, but normally it's better not to treat XML like plain text, or at least to be careful. Although XML files can be readable, they are more structured and reckless edits (like replacing the " character, which has special meaning) could corrupt the file. 

## Stage 3: Repackaging

After we are done with changing the files, we may want to put them back into the translation package. In this case, just make sure they are all in the same folder and then:

1. select them (you can press *Ctrl*{:.kbd}+*A*{:.kbd} in File Explorer);
2. select the `Share` tab from the upper menu;
3. click `Zip`.

<img src="{{ site.baseurl }}/assets/blogpost2/zipping_back_steps.jpg">

After you zip the files, the name of the resulting zip archive will be highlighted automatically, allowing you to easily change it. One caveat though – by default, the zipped folder has the same name as the **first of the files**:

<img src="{{ site.baseurl }}/assets/blogpost2/initial_rename.jpg">

...And we want it to have the same name as **the folder which contained the files**. Luckily, if we added the *.zip* extension at the very end, we can get the right name name easily.

Look at the bar above, where you have the full path to the file. Then left-click between the current folder name and the arrow icon (zone marked in red):

<img src="{{ site.baseurl }}/assets/blogpost2/adr_bar1.jpg">

The path will be selected in text form:

<img src="{{ site.baseurl }}/assets/blogpost2/adr_bar2.jpg">

You can now use your mouse/keyboard to select the last part (in my case, `idiom_tutorial_copy.xlz`), copy it and insert as the name of the zip file.

{:.info}
**The fast way**:  
After selecting, copy with *Ctrl*{:.kbd}+*C*{:.kbd}. Then left-click on the zipped folder, press *F2*{:.kbd} to enter the rename mode, *Ctrl*{:.kbd}+*A*{:.kbd} to select all text, *Ctrl*{:.kbd}+*V*{:.kbd} to replace it with the copied name. Then confirm with two *Enter*{:.kbd}s.

Excellent, now we have the modified files inside the zipped file, named the same way as the original package!

<img src="{{ site.baseurl }}/assets/blogpost2/final_look.jpg">

We can copy this package and either put it into an actual CAT tool for further processing or send it to our client in exchange for $$$ if our modifications were only some finishing touches :)

**Warning:**  
Instead of selecting the files and zipping them, you might feel tempted to zip the whole folder, so that it gets the name you want right away. **DON'T**! If you do this, your package will become one level deeper (`zip archive > folder > files` instead of the original `zip archive > files`) and CAT tools might not be able to open it.

## Conclusion

I have discussed in detail a rather popular workflow which allows you to get some files out of translation packages and modify them before they are loaded into a CAT tool... or to bypass the CAT tool altogether.

The main advantage of this workflow is that it does not require any special software, you can simply use the applications already installed by default on most Windows PCs (and probably on other systems as well – I can only speak for Linux Mint here!).

Its disadvantage is that it requires some mouse-clicking, typing and opening programs every time you want to work with a translation package. For this reason, it's not suited for tasks where you have to modify multiple packages. Sure, you can learn keyboard shortcuts, train your muscle memory etc., but you will eventually hit a wall.

However, with a little bit of scripting, we can easily break this wall down and handle any number of zipped packages! This is what the next post in this series will be about.

Until then, have fun handling your packages in creative ways! :)
