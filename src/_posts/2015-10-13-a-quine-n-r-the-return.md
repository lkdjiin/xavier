---
layout: post
title: "A Quine in R - The Return"
comments: true
---

In the previous post [A Quine In R](http://xavier.nayrac.eu/2015/10/10/a-quine-in-r/)
I presented a [quine](https://en.wikipedia.org/wiki/Quine_%28computing%29)
in the R programming language. The code was a little bit long for the task, 19 lines, mainly
compared to the Ruby code from the original post:

``` ruby
src = "\nputs \"src = \" + src.inspect + src"
puts "src = " + src.inspect + src
```

In Ruby, the code is short thanks to the method `inspect`, who automatically
escape the non printable characters and the quotes:

```irb
>> foo = "\nputs \"src\""
"\nputs \"src\""
>> foo.inspect
"\"\\nputs \\\"src\\\"\""
```

Naturally I searched for a similar function in R, at least for the strings.
I gave up after fifteen minutes of unsuccessful search, and I wrote
[the 19 lines of code](http://xavier.nayrac.eu/2015/10/10/a-quine-in-r/)
from the previous post.

At this moment, Hadley Wickham kindly suggested to use the function
`encodeString`. That's what I had been looking for, without finding it.
With the help of this function, a quine in R is really shorter. Not as
short as the Ruby version, but, anyway, it's shorter:

``` r
src <- "\nwriteLines(c(paste(\"src <-\", encodeString(src, quote='\"')), src))"

writeLines(c(paste("src <-", encodeString(src, quote='"')), src))
```

I like this version, so I add it on [rosettacode.org](http://rosettacode.org/wiki/Quine#R).

Like I said previously, it's good to use `diff` to assure yourself that you
really wrote a quine ;)

``` bash
diff -u quine2.r <(Rscript quine2.r)
```

And the result is:

```
$ Rscript quine3.r
src <- "\nwriteLines(c(paste(\"src <-\", encodeString(src, quote='\"')), src))"

writeLines(c(paste("src <-", encodeString(src, quote='"')), src))
```

