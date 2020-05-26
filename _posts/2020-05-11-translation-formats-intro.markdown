---
layout: post
title:  "File formats in CAT tools 1 - a gentle introduction"
date:   2020-05-11 13:50:25 +0200
categories: intro files XML
---

*This is a series of blog posts on file formats used by CAT (Computer-assisted translation) programs for storing translation data. Their aim is to share some knowledge which should allow us to tame our CAT tools better. Or to become independent from their whims.*

*This post discusses some basic facts related to XML and archive files. If you want to jump straight to editing them without a CAT tool, see [Part 2]({{ site.baseurl }}{% link _posts/2020-05-14-translation-formats-practice.markdown %}).*

## Common formats used in translation

Many programs for computer-aided translation use their custom file extensions: MemoQ's *.mqxliff* or *.mqxlz*, Trados' *.sdlxliff* and *.sdlproj*, the interoperable *.tmx*... This variety gives some translators the feeling that the files might be tied to the respective software and that they cannot be edited in other ways.

Luckily, that is not the case. Most of the time, we can access and modify the content of these files. Even without using any CAT tools. In this post, I will try to untangle some myths related to them.

{:.info}
**Note:**  
I will only focus on intermediate formats used directly by CAT tools. File formats we can import *into* our CATs (such as *.docx* or *.pdf*) will only be briefly mentioned. They have their own quirks and I will discuss them in separate posts.

Generally, we can divide most of file formats used by translation software into two categories: **XML files** and **archives**. The table below contains a summary:


|   | general | Trados | MemoQ |
|---|:---------:|:--------:|:-------:|
|**XML file**<br>*(Can be opened with a text editor)*| .tmx<br>.tbx<br>.xliff | .sdlxliff | .mqxliff |
|**Archive**<br>*(Has to be decompressed)*| .xlz | .sdlppx<br>.sdlrpx | .mqxlz |

Now, let's discuss the two basic types in more detail.

# XML files

XML (eXtensible Markup Language) is an incredibly widespread format for storing data and the basis of countless applications:

* Configuration data of Android apps? XML.
* Format for financial statements? XBRL, based on XML.
* Vector graphics? SVG, based on XML.
* Geolocation data? Often XML.

Many things in the world were built atop some tailored XML 😀 It has also become the most popular intermediate format for translation files.

As translators, we might be using a few kinds of XML-based formats or their derivatives: *.xliff* (for storing source-target pairs), *.tmx* (for translation memories) or *.tbx* (for glossaries).  
Custom formats, *.mqxliff* from MemoQ and *.sdlxliff* from Trados, are based on *.xliff* as well.

Here is an example of XLIFF file content:

{% highlight xml linenos %}
<xliff xmlns="urn:oasis:names:tc:xliff:document:2.0" version="2.0"
 srcLang="en-US" trgLang="ja-JP">

 <file id="f1" original="Graphic Example.psd">
  <skeleton href="Graphic Example.psd.skl"/>

  <!--The 1st translation unit, containing source and target.-->
  <unit id="1">
   <segment>
    <source>XLIFF Data Manager</source>
    <target>XLIFF データ・マネージャ</target>
   </segment>
  </unit>

  <!--Potentially more units...-->

 </file>
</xliff>
{% endhighlight %}
*(Example adopted from [the Wikipedia entry on XLIFF](https://en.wikipedia.org/wiki/XLIFF))*

&nbsp;

Some XML basics:

* The most notable part of XML structure are **tags**. We can distinguish between start (`<...>`) and end (`</...>`) tags.
* The first string of characters within the brackets (before whitespace) is the **name** of the tag.
* A pair of same-name tags and everything between them (text, other tags etc.) is called an **element**. It's the basic building block of XML. Elements can be nested in each other.
  
  Let's look at the `segment` element (lines 9-12). Its start tag is *\<segment\>* and the end tag is *\</segment\>*). It is contained in the `unit` element. It also contains two child elements: `source` and `target`. 

* Apart from the obligatory name, each element may contain **attributes**, which have some specific **values**.
* They may only be specified in the start tag. The end tag contains the name only.

  In this case, the attributes of the `file` element (line 4) are *id* and *original*. The value of the *id* attribute is *\"f1\"*. The value of the *original* attribute is *\"Graphic Example.psd\"*.

* Tag pairs without other content between them can also be written as a single tag, with a forward slash at the end.

  In our case, it's the `<skeleton (...) />` tag from line 5. It could have also been written as `<skeleton (...)></skeleton>`.

* Space between elements does not matter that much. The example was indented (*prettified*) for clarity, but the tags could have also been put in one line, one right after the other.

What is most interesting to us, as translators, are the `source` and `target` elements. They occur in many different bi- or multilingual files. The first type contains the original text, and the second one contains the translation.

&nbsp; 
&nbsp; 

# Archives

Archives are basically compressed folders which can contain multiple files. They might have different extensions, but in many cases **they are the popular .zip format under the hood**. Some files which, quite surprisingly, are actually archives:

* popular formats used by Microsoft Word (*.docx*), Excel (*.xlsx*) and PowerPoint (*.pptx*),
* their LibreOffice equivalents (*.odt*, *.odf* and *.odp*),
* applications for Android phones (*.apk*),
* and, of course, translation packages (*.xlz*, *.mqxlz*, *.sdlppx*...).

Unlike XML files, archives can't simply be viewed in your text editor. They contain compressed streams of data, which the text editor would try to directly convert into characters. This is what happens if you try to open an archive in Notepad:

<img src="{{ site.baseurl }}/assets/blogpost1/archive_mangled_in_notepad.jpg">

Most of the text is mangled and unreadable. The only readable text within the raw bytes are file names, such as the name of the single file I zipped in this case - *example_file.txt*, from line 2.

Sometimes, when browsing files in Windows Explorer or other file explorers, you can click on a *.zip* file and see its contents as if it were a normal folder. This is because **your operating system hides the complexity from you and unpacks the archive behind the scenes** (both Linux Mint and Windows 10 do it, from my experience).  
However, if you tried to open and edit the files without extracting them first, you could encounter trouble.

To demonstrate, I saved this blog post to my disk, choosing the *"Web Page, complete"* option. As a result, I got:

* a *(...).html* file,
* a *(...)_files* folder right next to it.

Then I packed them both into a zip archive. I opened both the original website and the one inside the archive by clicking on the *.html* files. They both opened in my browser. However, they looked different.  
Here is a side-by-side comparison:

<img src="{{ site.baseurl }}/assets/blogpost1/zipfile_mangle_illustration.jpg">

When my browser opened the file locked inside the archive, the image was not loaded and the text looked different.

This is because the *.html* file refers to some files from the folder next to it. **Even though we see the contents of the archive in the file explorers, our browser cannot access them**. So it can't e.g. load the stylesheets which dictate the look of the website. This is also why the text looks different - the browser cannot access formatting information, so it uses the default font. 

This example shows us that files inside an archive are not as accessible as outside of it. If you want to modify the files, you should decompress the archive, make your changes, and then re-compress the bundle again. This is also what your CAT tools do behind the scenes every time they open a package - there is no magic here.

In practice, archive files used by translators usually contain a bunch of XML files: bilingual files for translation, structure of the source file (or the file itself), translation memories, glossaries... They might also contain some other reference files.

## Some rules of thumb for dealing with files

Although the variety of file formats may seem daunting at first, they actually belong to a rather small set of categories and are subject to some universal rules.  
Here are the ones which made it much easier for me to feel comfortable around files:

**1. Files are just blocks of bytes**

   In practice, this means that two exactly identical files, opened by the same reliable software, will **always** appear exactly the same. In theory, you could write any file by hand. Sure, manual editing might be tedious and error-prone, but there is no magic in CAT tools which would force you to use them. 

**2. Files of the same type can be processed in the same way**

   > If it walks like a duck and it quacks like a duck, then it must be a duck.

   There are many file formats, but the number of actual standards is much lower - many files have a common stem. For this reason, all valid XML files can be parsed with an XML parser and all ZIP archives can be unzipped. Can't find any search results for some obscure .xyz format? Solution: recognize that .xyz is actually XML, use proven tools to parse the file and then adapt them to your use-case.

**3. File extensions are just a hint**
   
   If you manually change the extension of a file, you might see a warning pop up (on Windows) and the file icon change. This might make you think that the file was somehow converted. However, it wasn't. The name of the file, including the extension, is **separate from its content**.  
Some programs use custom file extensions to get distinct icons and treatment. But if their content is e.g. valid XML, then they can be opened perfectly fine as XML. Then point 2 applies.

**4. There are exceptions to all rules**

   Notice how I write *reliable software* or *valid XML*? Although the rules are universal, it's always possible to encounter something atypical or plain buggy. Don't let this discourage you from experimenting with file manipulation... but maybe don't do it right before a deadline! 😀 Having a plan B always helps. 

I hope this clarifies things a bit and gives you some confidence. CAT tool formats really are more accessible than they seem. Let's [apply our knowledge in real-life situations]({{ site.baseurl }}{% link _posts/2020-05-14-translation-formats-practice.markdown %})!

## Other resources

* [XML tutorial from W3C](https://www.w3schools.com/xml/)
* [A presentation by Angelika Zerfass discussing *.tmx*, *.tbx* and *.xliff*](https://www.zaac.de/pdf/2015_TLC_Warsaw_Zerfass_DataTransfer_with_tmx_tbx_and_xliff.pdf)
* [Wikipedia's summary of various archive formats](https://en.wikipedia.org/wiki/List_of_archive_formats#Comparison)
