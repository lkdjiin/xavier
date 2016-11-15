---
layout: post
title: Workaround for a Gvim Bug on Debian Sid
comments: true
---

Since an update of the gtk3 lib, there is a bug with the `gvim` command on
Debian Sid (and possibly other systems too).


## The Bug

Gvim is unusable! We you run the program you get this message, repeated many times:

    $ gvim

    (gvim:6054): Gtk-CRITICAL **: gtk_widget_set_size_request: assertion 'width >= -1' failed
    *** BUG ***
    In pixman_region32_init_rect: Invalid rectangle passed
    Set a breakpoint on '_pixman_log_error' to debug
    .
    .
    .

The bug will eventually be fixed either by the vim part or by the gtk3 part.
But in the meantime, what do we do?

## A Workaround

The program called by `gvim` is `vim.gtk3`, as you can see:

```bash
$ which gvim
/usr/bin/gvim
$ ls -l /usr/bin/gvim
[...] /usr/bin/gvim -> /etc/alternatives/gvim*
$ ls -l /etc/alternatives/gvim
[...] /etc/alternatives/gvim -> /usr/bin/vim.gtk3*
```

So we can use the «old» version `vim.gtk`. You maybe have to install it with
`apt-get install vim-gtk`.

Either run it manually with `vim.gtk -g` instead of `gvim`.

Or use `update-alternatives` to select which program to run with `gvim`:

    $ sudo update-alternatives --config gvim

You might prefer to use the graphic version of update-alternatives, `galternatives`.
