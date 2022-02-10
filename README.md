# Maths Club Website
Hi, I'm Garv! Welcome to the CGS Maths Club repository! <br>
This repo contains an archive of questions from the Jerry Mao Maths Club, and serves as a website for questions and solutions over time. <br>

Initially, the website was created by Junhua Chen, the administrator of the maths club at the time, located [here](https://cgsmathclub.herokuapp.com/).
This website included static blog posts from Jekyll, which pulled from [this website](https://maths-club.github.io) (repo [here](https://github.com/Maths-Club/Maths-Club.github.io)), and combined it with a quiz system written in Django to create a nicely functioning Maths Club website!

At the time, I was also on board with the project, adding little things here and there, and I was working on a little redesign at a fork I made [here](https://github.com/garv-shah/maths-club-test). <br>
I was going to implement the Django system eventually, but I got bored after the initial website stopped being maintained or used as much as it used to.

Fast-forward a bit, and now I'm in charge of the maths club with the help of a few friends, and I remembered the website we made and wanted to actually use it, instead of having it sit stagnant, not being maintained!
So, now we have this repo; I moved the contents of the fork into a new organisation which I can control, and redid the blog styling a bit. It's still only a Jekyll blog with LaTeX support (none of the quizzes or leaderboard stuff from before), but I might eventually re-implement something of the kind with a more modern, cleaner system like Firebase.

**TLDR:** This is a website for the CGS Jerry Mao Maths Club with a website link here: https://cgs-math.github.io

# How to Create Posts:
It's pretty simple, you just create a Markdown file (click [here](https://www.markdownguide.org/basic-syntax/) to learn more about the syntax) with the format YYYY-MM-DD-Title.md in the _posts folder.
Each file must be started with the following structure:
```
---
title: Insert Title
excerpt: Insert Excerpt
author: Insert Author
layout: post
---
{% include header.html %}
```
<br>
To include images or gifs, just upload the file to the static folder. This is where all of files will be hosted and can be accessed within the Markdown. The following line can be used:

```
![Name]({{ site.baseurl }}{% link static/filename %})
```

An example of which would be:

```
![Cat]({{ site.baseurl }}{% link static/cat.gif %})
```

This is done through the use of Jekyll's built-in tag system, which is useful but not exactly flexible. For more control, you can render HTML directly in the Markdown file, which works, but is just not ideal. Below is an example of the same cat gif from above, just bigger with HTML:

```
<img alt="Cat" src="https://github.com/cgs-math/club/blob/main/static/cat.gif" width="500"/>
```

Note that Markdown does not render inside HTML tags, so you'll have to use the HTML equivalent instead of the shortcuts.

## Maths:
Jekyll supports rendering maths with LaTeX. For more information on the syntax, you can visit https://en.wikibooks.org/wiki/LaTeX/Mathematics, with https://quicklatex.com allowing for some quick rendering since GitHub's built-in Markdown does not. <br>
[This](https://latex-tutorial.com/tutorials/amsmath/) guide also isn't bad if you'd like to figure out how LaTeX works, but honestly, just search up LaTeX on Google. Here's a quick summary:

### Summary of LaTeX:
Anything between dollar signs renders as Maths. For example:

```
$x + x = 2x$
```

Would render as the maths equation. Pretty neat, right?<br>
Similarly, you can use commands with a backslash prepended:

```
$\frac{1}{1}$
```

Would render the fraction 1/2. Note that unlike Markdown, LaTeX works within HTML tags (which is actually a life-saver)!<br>
This means that in solutions and the like that needs to be inside an HTML tag (solutions are inside details tags), even though you can't use the luxuries of markdown for photos etc., you can definitely use LaTeX to your heart's content. Check out the TestPost inside the _posts folder for more on this (or you can check out the rendered version [here](https://cgs-math.github.io/club/posts/TestPost))

# How it Works:
Essentially, the main website is just an RSS Reader, which loads the feed.xml generated by Jekyll (from feed: https://cgs-math.github.io/club/feed.xml). This then grabs the headers (title, excerpt and author) and creates a text box with the makeBlogPost() function that gets pushed into the main page. This is all done through the loadFeed.js file :D
<br> Everything should be automatically updated after uploading a post

## Summary of Jekyll
Jekyll is essentially a renderer that makes writing blogs much much easier. It lets you put in a Markdown file and produces a full html website. <br>
Markdown is a lightweight markup language, and in essence, it's very similar to writing a Word document, as most of it is just text, with a bit of syntax to tell the renderer what stuff is (https://www.markdownguide.org is a great resource to learn more about Markdown) <br>
As mentioned above, Jekyll goes slightly beyond the scope of Markdown, allowing for the rendering of Liquid and Textile out of the box, with support for other markup languages like LaTeX as well. <br><br>
At build time, Jekyll compiles all the files above and creates a few new directories. GitHub Pages (the host for this project) supports Jekyll natively, so above, you don't see the actual directory that is served to the user but rather a precompiled version. As an example of this, the "feed.xml" file mentioned above is nowhere to be found in the repo above, and is instead created by Jekyll on build. <br>
This being said, the website you see above isn't structured exactly like any Jekyll site, as in the actual "home page" doesn't use Jekyll at all. Rather, the page you see is an RSS reader. *Technically it's creating an Atom feed, but RSS and Atom feeds are similar enough to the point where for all practical purposes, it's the same thing.* <br>
This grabs the RSS feed that Jekyll has generated and serves up its own website. The advantage of this is that the home-page is much more "website like" and customisable, with the theming options evident, while still making the blogs very easy to publish. At the same time, it also presents the disadvantage of the whole codebase not being unified. This could be fixed if I just made a Jekyll theme based on the main website, but I haven't yet, though I plan to.<br>
Finally, when you click on the "Read More", it just redirects you to the pages that Jekyll *did* generate, which are the blog posts.

## The UI
The frontend UI of the website is quite honestly a mess of many different projects splashed together to create something that works. The main homepage is just a ***HEAVILY*** modified bootstrap theme. I've intermittently reused and worked on it throughout many projects, and it's gotten to quite a nice state. Namely, when I was doing my redesign with the fork, I added in some dynamic CSS theming, so if you click settings, you can modify basically all of the colours (using [pickr](https://github.com/Simonwep/pickr)) and some labels/icons of the website to make it your own. I used this to make some pretty cool looking presets, with smooth transitions between light and dark mode! <br>
Besides that, I used [this](https://github.com/andrewhwanpark/dark-poole) Jekyll theme for the internal blog posts, since the default GitHub ones were getting a bit old. Overall, the defaults look pretty nice right now, and I'm really happy with the CSS theming system I managed to build up. I hope to integrate it a lot more into Jekyll, so the global themes effect the blog posts as well, and also hopefully add a leaderboard/quizzes, which should make the gamification element of it a lot more fun!

## Build Locally
To be honest, it doesn't exactly matter if you create a post and push it directly to the main branch here, since you can always change it. Building locally is mostly useful for quick testing purposes, or debugging (GitHub doesn't give the best error results) <br>
**The below instructions are for a Mac, I'm not currently using a Windows/Linux device for development, and the people that this explanation was originally intended for didn't need it either. Therefore, I haven't written a guide for any other platforms. Also note that if the commands below don't work, prepending them with sudo may help** <br><br>
To start, first clone the GitHub repo from above. It's recommended to use an app such as GitHub Desktop, since the command line can be a bit daunting at first. Just install the app from here (https://desktop.github.com) and log in. You should see an option to clone a repository, and you can either paste the https link in or select it if it's there. <br>
Time for the terminal! This repo uses Bundler to manage all the dependencies. For this, you'll first need to install Ruby. You probably already have it installed.
If ```ruby -v``` returns anything besides the command ruby not being found, skip the next step, as you already have it. If not, use Homebrew, and type in ```sudo brew install ruby```.
<br>
Now to install Bundler. Just type in :

```
gem install bundler
```

Type in your password if required. Now navigate to the repository you cloned before using the cd command. If you used the default for GitHub Desktop, the command should be:

```
cd ~/Documents/GitHub/club/
```

Now run these two commands.

```
bundle config set --local path 'vendor/bundle'
bundle install
```

If all went well, it should have installed all the gem dependencies, and you should be good to go. Just run ```bundle exec jekyll serve``` and it should start hosting the site at http://127.0.0.1:4000/. Yay!

# Note:
The same blog system has been used for a few other projects of mine, namely the Nova System, an educational app to mimic cryptocurrency transactions. The main blog of [that repo](https://github.com/The-NOVA-System/blog) is basically the same as this one (I updated them in tandem), but it used to have a different design, accessible [here](https://the-nova-system.github.io/blog-old/). <br>
Check it out if you're interested, it just demonstrates that the system is nice and flexible to be used with essentially any UI.
