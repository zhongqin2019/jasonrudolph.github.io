---
title: "Defining Atom Commands in Your Init Script"
layout: post
tags:
- atom
---

I'm thrilled that [Atom](https://atom.io/)—the newly-announced text editor from GitHub—is now out in the wild for more people to enjoy. It's been my editor of choice for the past seven months. Atom is a delight to use. And for the first time, I'm using an editor that I find enjoyable to *extend*. There's a ton to say about Atom, but for the moment, let's talk about a quick way to start experimenting with extending the default Atom experience.

The majority of your Atom customizations will come in the form of [packages](https://atom.io/packages). Packages provide an excellent means for defining commands and other customizations. [1] But sometimes I want to quickly define a new command without [creating a full-blown package](https://atom.io/docs/v1.0.2/hacking-atom-package-word-count). Cue [`~/atom/init.coffee`](https://atom.io/docs/v1.0.2/hacking-atom-the-init-file).

## Defining your first command

As a simple (and admittedly contrived) example, let's define a command that logs a message to the console. For starters, add the following code to your `~/atom/init.coffee` script:

{% highlight coffeescript %}
atom.commands.add 'atom-workspace', 'dot-atom:demo', ->
  console.log "Hello from dot-atom:demo"
{% endhighlight %}

Atom evaluates `init.coffee` each time you open a new window. To test out this new command, you can open a new window, or you can reload the current window via the "Window: Reload" command in the [Command Palette](https://atom.io/docs/v1.0.2/getting-started-atom-basics#command-palette).

Now, use the Command Palette to locate and execute the new command by name (i.e., "Dot Atom: Demo"), as shown in the gif below. Each time you run the command, you'll see the message logged to the console.

Defining and using a new command is just that simple.

If you'd like to trigger the command via a keyboard shortcut, you can define a keymap for the command in [`~/.atom/keymap.cson`](https://atom.io/docs/v1.0.2/using-atom-basic-customization#customizing-key-bindings).

[<img src="/resources/201403-define-atom-commands-in-your-init-script.gif" alt="Demo of an Atom command in init.coffee" title="Demo of an Atom command in init.coffee"  width="100%" />](/resources/201403-define-atom-commands-in-your-init-script.gif "Demo of an Atom command in init.coffee")

## Going further

Because `init.coffee` provides full access to Atom's API, it's fertile ground for implementing genuinely useful commands. For example, Lincoln Stoll uses his `init.coffee` to define a [command for generating ctags](https://github.com/lstoll/.atom/blob/557394111a8f16b5f3efa9800fe37682ec71689a/init.coffee#L13-L29). In my `init.coffee`, I define a [command that closes all panes in one fell swoop](https://github.com/jasonrudolph/dotfiles/blob/86ec9226fbede526006a8be537dc77152e4a17cd/atom/init.coffee#L28-L37), and I'm experimenting with [a few other commands](https://github.com/jasonrudolph/dotfiles/blob/86ec9226fbede526006a8be537dc77152e4a17cd/atom/init.coffee#L43-L115) as well. [2]

Whether you need a sandbox for experimenting with new commands before publishing them in
a package, or you just want to define a few small commands without the overhead of an entire package, `init.coffee` is the place to go.

## Notes

[1] I've enjoyed writing a [handful](https://atom.io/packages/open-on-github) [of](https://atom.io/packages/sort-lines) [packages](https://atom.io/packages/toggle-quotes) over the past few months. Now that Atom is in public beta, the package ecosystem is quickly [heating up](https://atom.io/packages/list).

[2] As people begin to share their Atom [dotfiles on GitHub](http://dotfiles.github.io/), it's going to be a blast to discover novel customizations that allow developers to get even more from Atom.