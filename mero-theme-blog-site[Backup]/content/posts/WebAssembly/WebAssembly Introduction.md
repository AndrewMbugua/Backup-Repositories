+++
date = "2020-09-11T10:54:24+02:00"
draft = false
title = "WebAssembly Introduction"
slug = "post-title"
tags = ["Linux","WebAssembly"]
image = ""
comments = true	# set false to hide Disqus
share = true	# set false to hide share buttons
menu= ""		# set "main" to add this content to the main menu
author = "Andrew"
+++

```bash
I won’t say that I know much about WebAssembly since I am just beginning to use it as of this writing

I became caught up with all this WebAssembly hype and how it’s the next big thing that is going to transform the web
so I decided to give it a try.I am not going to attempt to go very deep into what it is but what
I am going to do is to give a beginner level lesson of starting to use it.

What WebAssembly aims to do is to provide a chain to compile languages such as:
Rust,C,C++ directly to web assembly and thus allow web developers to write in the language of their choice
and run it inside a browser.WebAssembly also aims to make things blazzingly fast as it’s name inspired by the Assembly Language.

I have listed the prerequisites for Web assembly,to run a basic example like hello.cpp,you will have to type this in the terminal:
$ emcc hello.cpp -s WASM=1 -o hello.html
for newbies like me (as of this writing) the *emcc command was not found* so I had to go to the Emscripten website and find the installation instructions.
But not to worry,I have chosen to simply lay it out for you below:

$ git clone https://github.com/emscripten-core/emsdk.git

$ cd emsdk

$ git pull

$ ./emsdk install latest

# Make the “latest” SDK “active” for the current user (writes .emscripten file)
$ ./emsdk activate latest

# Activate PATH and other environment variables in the current terminal
$ source ./emsdk_env.sh

# Note: My default development environment is Linux.
Other prerequisite tools needed but ones that normally come preloaded on most linux distributions include python3,
cmake and git but if your chosen distribution doesn’t have them(which I doubt) type these.
$ sudo apt-get install python3
$ sudo apt-get install cmake
$ sudo apt-get install git-core

After doing all that now run the initial lines again.

$ emcc hello.cpp -s WASM=1 -o hello.html
  3 files are generated:
- hello.html
- hello.js
- hello.wasm
Upon opening the generated html file, a webpage powered by emscripten will pop-up in your default browser.

And now…The let Journey begin.


```
