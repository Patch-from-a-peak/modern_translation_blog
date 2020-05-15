---
layout: post
title:  "OCR without ABBYY Fine Reader"
date:   2020-05-15 12:41:25 +0200
categories: jekyll update
---

There are many helpful applications - but some of them seem irreplaceable. The time savings they give us are so big that it is hard to imagine life without them.

An example of such an application is ABBYY Fine Reader, used for OCR (*Optical Character Recognition*) - recognizing text on images and converting it to a digital form we can edit, or translate, on our computers.

Without OCR software, we would either have to write our translation on-the-fly, without benefitting from translation memories, or transcribe the original text and THEN translate it with our CAT software. Which would probably consume even more time.

So I can't really replace OCR with manual labor. Is paying 200 $ for ABBYY's cheapest version the only solution I have?

No. Luckily, some great Python scripts come to the rescue.

## Fixing line splits

One problem we might encounter 

```python
import re

def fix_false_line_splits( text ):
    
    line_end_chars = '([a-z,:;])'
    line_start_chars = '([a-z])'

    broken_lines = '{}\n{}'.format( line_end_chars, line_start_chars )
    merged_lines = '\g<1> \g<2>'
    
    return re.sub( broken_lines, merged_lines, text )
```

Let's try it out with an example:

```
example = '''
This sentence
should be one.
But it was divided,
such a shame.'''

fixed = fix_false_line_splits( example )
print(fixed)
```

Perfect! It merges the text nicely/

```
This sentence should be one.
But it was divided, such a shame.
```

**Learning from mistakes:**
You might wonder about the `'\g<1> \g<2>'` line. My previous version was `\1 \2`; it did merge the lines, but interpreted the characters differently than I thought and replaced both start and end characters with ``. I searched for "python re sub how to refer to groups" and found the solution in [this SO question](https://stackoverflow.com/questions/5984633/python-re-sub-group-number-after-number))*.


