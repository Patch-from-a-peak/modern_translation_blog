---
layout: post
title:  "Working with PDF 1 - merging lines"
date:   2020-05-16 00:03:25 +0200
categories: jekyll update
---

PDF files are the nemesis of many translators. They look so deceptively simple when opened in a viewer: there is text, it can be selected. But we see no way of 

One of my favorite little scripts is a simple one for merging

```python
import re

def fix_false_line_splits( text ):
    
    line_end_chars = '([a-z,:;])'
    line_start_chars = '([a-z])'

    broken_lines = '{}\n{}'.format( line_end_chars, line_start_chars )
    merged_lines = '\g<1> \g<2>'

    return re.sub( broken_lines, merged_lines, text )
```

Let's try our script in practice!

```python
#Example:
example = '''
This sentence
should be one.
But it was divided,
such a shame.'''

fixed = fix_false_line_splits( example )
print(fixed)
```

It works as it should, great! We now have a function

Let's make `start_chars` and `end_chars` arguments of the function. This way, we can explicitly provide them. But if we make it necessary to specify them, users will have to do it all the time... so let's assign our previous characters as default values.

```python
def fix_false_line_splits( text,
                           line_end_chars='([a-z,:;])',
                           line_start_chars='([a-z])' ):
    
    #The rest stays the same...
```

This way, we have created **a customizable function**. Usually, we won't pass any `start_chars` or `end_chars` into it, so they will go into the function as `None`s and our reasonable default values will be assigned to them. But if we DO have a need to adapt the function, we can easily override the defaults. Such generalizations are something which occurs over and over again as you script up your life.

Let's test the function in practice. Say we have this example of text from a PDF:

```python
example2 = '''
Some people believe that editing PDF files
is easy if you can get the text, e.g.
by copying it to Notepad.
However, many have been unpleasantly surprised
when the "easy 5-minute task" took ca.
30 minutes of intense editing.
If only they knew scripting...'''
```

In this case, our script would merge two of the lines, but fail at the ones starting after *e.g.* and *ca.*. The reason is clear - there is no full stop among our `start_chars`, so a sequence of `(full stop)(newline mark)(lowercase letter)` will not be matched by regex. And rightfully so, because a full stop can indicate the end of a sentence, so line breaks after it are justifiable!

This is a very similar dilemma to the one CAT tools have during sentence tokenization - they don't know all abbreviations and other exceptions, so we sometimes have to provide additional rules by ourselves. Except in this case our CAT tools would not help. They always divide on line breaks first and apply sentence segmentation later.

Conclusion - if we don't want the sentences to be split, we have to change the merging rules right here, in our script, before we load anything into the CAT tool.

```python
default_pattern = '[a-z,:;]'
abbrev_pattern = '| e\.g\.| ca\.'
new_pattern_before_break = '(' + default_pattern + abbrev_pattern + ')'
```

Note that `start_chars` are a group with a single element, `[a-z,:;]`. If we want to add more potential matches to the group, we have to keep them within the round brackets, joined with the vertical line, \|. This is why the `abbrev_pattern` variable includes a vertical line before each element.

We also escape the full stops, because they have a special meaning within regexes, which we do not want. Finally, I have explicitly specified a single whitespace before a character, so that it only catches the abbreviations and not characters at the end of some word.

Let's use the function with our modified regex pattern:

```python
merged = fix_false_line_splits( line_end_chars=new_pattern_before_break)
print(merged)
```

We get the result we wanted, 3 segments instead of 7:

> Some people believe that editing PDF files is easy if you can get the text, e.g. by copying it to Notepad.  
> However, many have been unpleasantly surprised when the "easy 5-minute task" took ca. forty minutes of intense editing.  
> If only they knew scripting...

Success! As you can see, the function merges the segments as it should by taking in our requested abbreviations. And we could generalize it even further by adding other abbreviations to the `abbreviations` variable, perhaps programmatically.

But, let's stop at that. We already have a basic but working solution which can save us some trouble when preparing unruly text for translation.

You can find the complete script [here]. Happy editing and till the next time!
