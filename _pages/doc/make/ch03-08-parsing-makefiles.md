---
layout: framework
title: 3.8 How Makefiles Are Parsed
permalink: /doc/make/ch03-08-parsing-makefiles.html
---

## 3.8 How Makefiles Are Parsed

GNU make parses makefiles line-by-line. Parsing proceeds using the following steps:

1. Read in a full logical line, including backslash-escaped lines (see Splitting Long Lines).
2. Remove comments (see What Makefiles Contain).
3. If the line begins with the recipe prefix character and we are in a rule context, add the line to the current recipe and read the next line (see Recipe Syntax).
4. Expand elements of the line which appear in an immediate expansion context (see How make Reads a Makefile).
5. Scan the line for a separator character, such as ‘:’ or ‘=’, to determine whether the line is a macro assignment or a rule (see Recipe Syntax).
6. Internalize the resulting operation and read the next line.

An important consequence of this is that a macro can expand to an entire rule, if it is one line long. This will work:

```makefile
myrule = target : ; echo built

$(myrule)
However, this will not work because make does not re-split lines after it has expanded them:

define myrule
target:
        echo built
endef

$(myrule)
```

The above makefile results in the definition of a target ‘target’ with prerequisites ‘echo’ and ‘built’, as if the makefile contained target: echo built, rather than a rule with a recipe. Newlines still present in a line after expansion is complete are ignored as normal whitespace.

In order to properly expand a multi-line macro you must use the eval function: this causes the make parser to be run on the results of the expanded macro (see [The eval Function]()).