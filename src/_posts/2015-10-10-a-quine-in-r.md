---
layout: post
title: "A Quine in R"
comments: true
---

I just read the article
[generating Quines in Ruby](http://blog.chaps.io/2015/10/01/generating-quines-in-ruby.html)
and I really enjoyed it. I wanted to do a quine myself in R.

So, what's a quine? A quine is a self reproducing software. It must meet
two conditions:

1. It produces its source code as its unique output.
2. It doesn't take any input (thus excluding the ability to read from a file).

Here is my solution in R. It displays its source code on standard output when
executed. It is mostly inspired by the C code from the original article:

```r
src <-"\nescape <- function(x) {\n    cat('\"')\n    for(e in strsplit(x, '')[[1]]) {\n        if(e == '\\n') {\n            cat('\\\\n')\n        } else if(e == '\\\\') {\n            cat('\\\\\\\\')\n        } else if(e == '\"') {\n            cat('\\\\\"')\n        } else {\n            cat(e)\n        }\n    }\n    cat('\"')\n}\ncat(\"src <-\")\nescape(src)\nwriteLines(src)"
escape <- function(x) {
    cat('"')
    for(e in strsplit(x, '')[[1]]) {
        if(e == '\n') {
            cat('\\n')
        } else if(e == '\\') {
            cat('\\\\')
        } else if(e == '"') {
            cat('\\"')
        } else {
            cat(e)
        }
    }
    cat('"')
}
cat("src <-")
escape(src)
writeLines(src)
```

As noted in the original article, it's a good practice to test one's own
solution with `diff`. If the output of your quine and its source are identical,
`diff` will not produce any output, else, happy debugging ;)

``` bash
$ diff -u quine.r <(Rscript quine.r)
```

My solution is much longer than the one on
[rosetta code](http://rosettacode.org/wiki/Quine#R)
for example. But who care's? It was funny to do and it was a good little puzzle
to solve. And I even learn a new function of R (`writeLines`).

So it's up to you now. Let me know if you write a quine, whatever the language ;)
