---
layout: post
title: "Fish : completion and execution in just one time"
comments: true
---

Here is a tip for Fish, [the friendly shell](https://fishshell.com/), to complete a command line a execute it in just one time.

## Default behavior : completion then execution

Fish offers automatic completion as long as you're typing a command.
In the following screenshot, the grey part has not been typed yet. It is only
suggested by Fish.

<img src="{{site.baseurl}}/public/images/fish-shell-before-completion.png" class="" />

To accept the suggestion, one have to use the keyboard shortcut Ctrl+F. Then the cursor moves to the end of the line.

<img src="{{site.baseurl}}/public/images/fish-shell-after-completion.png" class="" />

Finally one can push Enter to run the command.

# And now a single shortcut

Fish's automatic completion is very good. But this two-step behavior, Ctrl+F then Enter, quickly exasperated me.
So I wanted to reduce it to a single shortcut : Ctrl+G.
Of course you can choose another key combination (I choose G because it reminds me «Go!»).

You need to create a function named `fish_user_key_bindings`, or add the following code to it if it already exists.
Put this function in the file `~/.config/fish/functions/fish_user_key_bindings.fish`.

```
function fish_user_key_bindings

    # Ctrl+g (Go!). Like Ctrl+f Enter in one go.
    bind \cg accept-autosuggestion execute

end
```

*Et voilà !*. It's only a line of code but I could not live without it.

If you too have a Fish's tip, please share it in a comment below and thank you in advance.
