---
layout: post
title: Better Use of the Gem Command
---


`gem` is a well known command amongst rubyists, for a good reason:
it is central to the use of Ruby.
As an example, if I want to benefit from 
[awesome print](https://github.com/michaeldv/awesome_print) in my irb session,
I will install it like this:

    $ gem install awesome_print

Likewise, did you ever see a Rails app without a Gemfile?

``` ruby
source 'https://rubygems.org'
ruby '2.0.0'

gem 'rails', '4.0.0'
gem 'pg'
...
```

Actually if you have only 3 days of Ruby in your life, you can use `gem` like
a boss. Do you? I don't. Not yet.

Indeed I use Ruby every single day since 5 or 6 years. And I had never written
`gem --help`. Never. Not once.

    $ gem --help
    RubyGems is a sophisticated package manager for Ruby.  This is a
    ...
      Further help:
        gem help commands            list all 'gem' commands
        gem help examples            show some examples of usage
        gem help gem_dependencies    gem dependencies file guide
        gem help platforms           gem platforms guide
        gem help <COMMAND>           show help on COMMAND
        gem server                   present a web page at
    ...

I think there is a lot to read. So, here is a quick tour of the many possibilities of `gem`.

## gem help commands

Let's start by looking at the different commands:

    $ gem help commands
    GEM commands are:

        build                  Build a gem from a gemspec
        cert                   Manage RubyGems certificates and signing settings
    ...
        wrappers               Re run generation of environment wrappers for gems.
        yank                   Remove a pushed gem from the index
    ...
    Commands may be abbreviated, so long as they are unambiguous.

I have abbreviated the previous output, because there are **33 commands**.
I really had no clue of such a big number of commands. Here is the list:

- build
- cert
- check
- cleanup
- contents
- dependency
- environment
- fetch
- generate_index
- help
- install
- list
- lock
- mirror
- open
- outdated
- owner
- pristine
- push
- query
- rdoc
- regenerate_binstubs
- search
- server
- sources
- specification
- stale
- uninstall
- unpack
- update
- which
- wrappers
- yank

Personnaly I already used `build`, `cleanup`, `install`, `list`,
`push`, `uninstall`, `update` and that's it! 7 commands on 33.
I am off the mark.

Looking closer to the output of `gem help commands`, I realize that one can
abbreviate each command:

    $ gem install my_gem

thus will be identical to:

    $ gem i my_gem

I really like this idea.

## gem help a_command

One can get some help for a specific command.
For example, with `gem help install` I learn that those options to not generate
the documentation:

    --no-rdoc
    --no-ri

are deprecated! Now one can use:

    -N, --no-document

## gem help examples

Obviously `gem help examples` displays several examples ;)
Like how to install a specific version of a gem:

    $ gem install rake --version 0.3.1

I don't know why but I never remember this syntax
Now I would not need to ask to a search engine.
I content myself with `geme help examples`.

## gem server

Here is a little curiosity: `gem server` provides an html page (see it at
`localhost:8808`) with the list of all installed gems.
This seems a little gadget, especially that one can have such information quickly on the command line with `list`:

    $ gem list

    *** LOCAL GEMS ***

    awesome_print (1.6.1)
    bigdecimal (1.2.6)
    bundler (1.7.9)
    ...

Then, with `gem help list`, I found a way to get details about installed gems:

    $ gem list -d

    *** LOCAL GEMS ***

    awesome_print (1.6.1)
        Author: Michael Dvorkin
        Homepage: http://github.com/michaeldv/awesome_print
        License: MIT
        Installed at: /home/xavier/.rvm/gems/ruby-2.2.0

        Pretty print Ruby objects with proper indentation and colors

    bigdecimal (1.2.6)
        Authors: Kenta Murata, Zachary Scott, Shigeo Kobayashi
        Homepage: http://www.ruby-lang.org
        Installed at (default): /home/xavier/.rvm/rubies/ruby-2.2.0/lib/ruby/gems/2.2.0

    Arbitrary-precision decimal floating-point number library.

    ...

## Need more work…

I didn't finish to read this documentation. It looks promising to me, and I
feel that I'm going to still learn many things.

See you soon.
