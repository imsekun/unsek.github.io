---
layout: post
title:  "Installing Elixir and Erlang in Solus"
date:   2020-05-22 14:04:12 +0800
categories: elixir erlang solus asdf-vm
---

# Why Solus

Until yesterday I've been using Ubuntu for a while and I sometimes switch to Solus here and there. Ubuntu is just too convenient for a lot of things since they have a vast collection of packages available to install with `apt`. However, although Ubuntu's performance has improved in the last few iterations, especially in 20.04, it still has much left to be desired. My only issue with Solus is that the Elixir and Erlang packages weren't up to date (last I checked) and my work depends on the latest versions of those. It was a problem until I discovered `asdf-vm`.

# What's asdf-vm

`asdf-vm` makes it convenient for you to manage versions of plugins. Plugins are essentially the tools you want to install. e.g Ruby, NodeJS, Elixir, Erlang, etc. These plugins have to be added first before you can install the tool itself. 

Oh, also I've submitted a [PR](https://github.com/asdf-vm/asdf-erlang/pull/146) for `asdf-erlang` in case you're wondering why it's not in their README. Not sure when it'll be reviewed but hopefully it'll be merged soon.

# Installation

## Erlang

Install the build tools
`sudo eopkg it -c system.devel`

For building wxWidgets
`sudo eopkg install wxwidgets-devel mesalib-devel libglu-devel`

For ODBC support
`sudo eopkg install unixodbc-devel`

For jinterface
`sudo eopkg install openjdk-8-devel`

If you want to install all of the above

```bash
sudo eopkg it -c system.devel
sudo eopkg install wxwidgets-devel mesalib-devel libglu-devel unixodbc-devel openjdk-8-devel
```

After installing the dependencies, you can now install and add Erlang to your system.

```bash
asdf list erlang # View all versions of Erlang
asdf install erlang <VERSION> # Substitute <VERSION> with a version in the previous step
asdf global erlang <VERSION> # Add the Erlang version to your global namespace
```

That's it! You can test it out with `erl`.

### Dealing with OpenJDK issues on Solus

I ran into an issue where `javac` wasn't a recognized command in the terminal despite having installed `openjdk-8` and `openjdk-8-devel`. Turns out it wasn't added to `PATH` by default. So simply add it to `PATH` like so:

```bash
# In ~/.bashrc add these to add Java to PATH
JAVA_HOME=/usr/lib64/openjdk-8
PATH=$PATH:$JAVA_HOME/bin
# In terminal
source ~/.bashrc
```

## Elixir

For Elixir things are much simpler since there are no extra dependencies you have to install.

```bash
asdf list elixir # View all versions of Elixir
asdf install elixir <VERSION> # Install a specific Elixir version
asdf global elixir <VERSION> # Add the Elixir version to your global namespace
```