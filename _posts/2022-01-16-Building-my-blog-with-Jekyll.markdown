---
layout: post
title:  "Building my blog with Jekyll"
date:   2022-01-15 18:00:00 +0100
categories: general, jekyll
description: "The title prettty much says it. I am going to show how I have started to build my blog and why I chose Jekyll to do it."
tags: "blog, programming, code, jekyll, wordpress "
---

# {{ page.title }}
Published: {{page.date | date: "%d-%m-%Y"}}


Whenever someone thinks about writing a blog, there is a good chance one will get to start with WordPress. The Content Management System
was also a good start for me when I began my journey into web development. I still think it has its place, but I've encountered many things I wanted to get rid of during the years. So, let me list the major points that made me switch from WordPress to Jekyll.  
<br>

**1. It's free**

'But Worpress is also free!?' - you could ask. While that's true, I noticed that more and more features within WordPress started to cost money, or one gets some real basic free version of a 'premium' tool. When I couldn't script that well, that change became a huge problem. Not only did I need to test several plugins/themes to find one that satisfies my needs, but I also had to consider if a tool was worth its money. 
<br><br>

**2. No Database**

Due to its serverless approach, Jekyll doesn't need a database to communicate with all the time. While that takes away some possible use cases, like adding a comment section or user registration, it raises my page's security since no writing operations are being sent to my server. 
<br><br>

**3. It's green-ish**

The web should also become greener. One way to reduce emissions is by reducing the number of requests that need to be sent between server and client. For example, Jekyll only loads the static content from the server, and that's it. On the other hand, WordPress typically does a lot of work in the background with all kinds of plugins that send or receive requests many times.
<br><br>

**4. Easy hosting**

I've hosted sites on different platforms it was alyways at least okay. When I got to know that I can host my own website on Github, that got me curious. Since I've started my first Jekyll project, I try to host all small sclae projects via [GitHub Pages](https://pages.github.com/)


<br>
## Setting up Jekyll
Since I've got used to working on Linux pretty much, I've set up WSL on my Windows machine and connected via Visual Studio Code with the Plugin [Remote WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl#:~:text=The%20Remote%20%2D%20WSL%20extension%20lets,as%20you%20would%20from%20Windows.). To get Jekyll running, I've followed [Colin Westwater's Tutorial](https://www.vgemba.net/blog/Setup-Jekyll-WSL/), which you can follow but here are also the lines you need to enter:

```
sudo apt install -y ruby-full build-essential zlib1g-dev
```

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```
gem install bundler jekyll
```

<br>
## Starting a new project
To start your new project, switch into your project directory and enter the following line and replace \<project-name\> with the actual name your project is supposed to have. The last line is going to open a test server on your local directory. For further help just follow the [Jekyll Tutorial]( https://jekyllrb.com/docs/).

```
jekyll new <project-name>
cd <project-name>
bundle exec jekyll serve
```

<br>
## Troubleshooting
In case you get an error message during the installation of Jekyll, and it says

```
Gem install wrong number of arguments (given 4, expected 1)
```

there is probably a problem with the psych package. To get rid of this error, enter the following lines in your console to deinstall psych, which is not necessary for using Jekyll:

```
sudo gem uninstall psych
sudo gem uninstall -i /var/lib/gems/2.5.0 psych
```