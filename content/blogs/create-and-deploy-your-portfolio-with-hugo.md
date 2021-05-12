+++
title = "Create and Deploy your portfolio with Hugo"
type = ["posts","post"]
tags = [
    "git",
    "gh-pages",
    "hugo",
    "portfolio",
]
date = "2021-02-04"
series = ["Hugo 102"]
[ author ]
  name = "Yeganathan S"
+++

Hello everyone 👋🏻

Have you just thought of making a portfolio or any static site then you're in the right place. In this article, I'm gonna share my experience ( also experiment ) with **Hugo**.

But before getting into it, let me give a brief introduction about Hugo...

#### What is Hugo?

Hugo is a general-purpose website framework. Technically speaking, Hugo is a static site generator. Unlike systems that dynamically build a page with each visitor request, Hugo builds pages when you create or update your content. Since websites are viewed far more often than they are edited, Hugo is designed to provide an optimal viewing experience for your website’s end users and an ideal writing experience for website authors.

#### What we are going to do?

We're gonna take a theme and customize as per our needs and deploy it on Github pages.

#### Why Github pages?

This is one of the easiest and simplest way of all. But still, we can also do the same in any other services like Netlify, Heroku and etc.

## Prerequisites 🚀
* Hugo and Git should be installed. if you didn't install it yet, then check out the following links.

[1] - [Installation of Hugo](https://gohugo.io/getting-started/quick-start/)

[2] - [Installation of Git](https://www.atlassian.com/git/tutorials/install-git)

* A Github account and knowledge of basic git commands.

To make it simple, I have made this blog into step by step process just like farming 🍀

**Let's start making wonders with Hugo 🎉**
## Preparation of soil 🪵
The best part of Hugo is, we can take a theme and pretty much work on it just like a word doc. so I have chosen a template already if u didn't yet, then go and find one for yourself  [here](https://themes.gohugo.io).

This is the template I have chosen for today's demo [Hello-friend-ng](https://github.com/rhazdon/hugo-theme-hello-friend-ng) 💐

#### Sneak peek of it 🤩

![Template](https://dev-to-uploads.s3.amazonaws.com/i/2tnarvwgxz88k3attm3x.png)


#### Note:
Github pages can't render Hugo files directly so we will be creating 2️ repositories. Once we complete making changes in the template, Hugo helps us to generate static files. The reason for the 2️ repositories is that one is used for Hugo files and the other for static files generated out of it.

Hope you have installed Hugo & git already, now it's time to fire up your terminal.

Type the following command,

```
$ hugo new site quickstart
```
> quickstart - it's just a directory name the files will be created.
After doing the same now, if you check out the quickstart directory you will be seeing some files/folders. Those are necessary files required for any hugo site and hugo generates those for us.

Now let's move into the quickstart directory and import the theme,
```
$ cd quickstart
$ git init
$ git submodule add <them_github_repo_link>
```
> Note: An empty git repository is initialized inside the quickstart directory so that we can add the theme as a submodule.

Now when you check the themes directory you will be seeing all those files of our theme.

## Sowing ⚙️

There will be an examplesite folder inside the themes directory, copy and **replace** all the contents of examplesite under project directory ( or outside of themes directory )

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/l8cwqvtcrzeiemmh7sgg.png)

When it comes to hugo, config.toml is the main file for our site.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/yyg3xz29yb3cj20z2xc7.png)

Look at the config.toml file and change the necessary details in it except the baseURL.

We can find a description/comments of each variable inside the config.toml so that we can make changes without messing up with the other things.

```
baseURL = "localhost"
```
>baseURL should be always localhost before deployment. 

## Prototype 🔫

Shoot up the terminal now...
```
$ hugo server
Start building sites … 

                   | EN | FR  
-------------------+----+-----
  Pages            | 35 | 21  
  Paginator pages  |  0 |  0  
  Non-page files   |  0 |  0  
  Static files     | 12 | 12  
  Processed images |  0 |  0  
  Aliases          | 18 |  7  
  Sitemaps         |  2 |  1  
  Cleaned          |  0 |  0  

Built in 65 ms
Watching for changes in /Users/yeganathan/quickstart/{archetypes,content,data,layouts,static,themes}
Watching for config changes in /Users/yeganathan/quickstart/config.toml
Environment: "development"
Serving pages from memory
Running in Fast Render Mode. For full rebuilds on change: hugo server --disableFastRender
Web Server is available at http://localhost:1313/ (bind address 127.0.0.1)
Press Ctrl+C to stop
```
Open a browser and enter the webserver address (localhost) to see the changes made. We can also make changes/ add content once we start our live local server and see the result instantly, this makes it even easier since we can see the result once we save our file with each change made.

We can also edit the core components of the theme by editing the required file for the required component inside the themes directory.

## Adding manure and fertilizers 🌱

We can also add few more components other than in the theme...

For instance,

If we need an extra menu (Photography) apart from the one given in the theme, we can easily make one by editing the config.toml

```
[menu]
  [[menu.main]]
    identifier = "about"
    name       = "About"
    url        = "about/"
  [[menu.main]]
    identifier = "posts"
    name       = "Posts"
    url        = "posts/"
  [[menu.main]]
    identifier = "photography"
    name       = "Photography"
    url        = "photography/"
```
> also, the contents of the page can be added to the content directory same as posts.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/9easomzpwjnk6tk7knts.png)

Basically, we can add anything that we want on our site. Just go around the files and start doing wonders ✨

## Irrigation 📦

So for we made changes to our site and the files are only in our local system, in order to deploy in web it should be stored in remote right!? here comes **Github**.

As said already we need 2️⃣ repos for our hugo site.

Create your 2️⃣ remote repos on Github, one as **[username].github.io** and the other as **quickstart**.

>⚠️ Remember ⚠️ 
The **quickstart** is nothing but the project_name we can always use anything of our own but keep in mind that it should be uniform throughout the process.

when creating [username].github.io repo always includes file .gitignore so that it won't shoot an error.

Inside the .gitignore file,
```gitignore
categories/*
tags/*
```
Write the following commands in terminal...
```
$ git remote add origin https://github.com/<github_username>/quickstart.git
$ git add .
$ git commit -m "Initial commit for our Hugo site."
$ git submodule add https://github.com/<github_username>/<github_username>.github.io.git
$ git add .
$ git commit -m "Initial commit for our generated HTML."
$ git push -u origin master
```

> this only pushes to quickstart repo.

We still need to generate our HTML pages for our [github_username] repo, but before generating we need to change our config.toml file to output our HTML files to our submodule [github_usernam].github.io.

Open your config.toml

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/0nxm78ogsl53q676wc68.png)

Change these things to as shown below...

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/oegkzvv7fcts8ax5qrvh.png)

Hugo already has a built-in command, that generates your files to a Public folder.

Let’s generate them by running the following command,
```
$ hugo
Start building sites … 

                   | EN | FR  
-------------------+----+-----
  Pages            | 35 | 21  
  Paginator pages  |  0 |  0  
  Non-page files   |  0 |  0  
  Static files     | 12 | 12  
  Processed images |  0 |  0  
  Aliases          | 18 |  7  
  Sitemaps         |  2 |  1  
  Cleaned          |  0 |  0  

Total in 136 ms
```
And that should be it. If you look in your [github_username].github.io folder now you should see HTML and CSS files, stuff that Github pages understand❗️

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/79c2pvx2mqdmboh12plw.png)


Before we finally deploy, we need to make sure our remotes are set up correctly.

```
$ cd <github_username>.github.io
$ git remote -v
> origin https://github.com/<github_username>/<github_username>.github.io.git (fetch)
> origin https://github.com/<github_username>/<github_username>.github.io.git (push)
```

Now after doing the above, you should probably see the same fetch and push.

## Harvesting 🌾
We are gonna push all those generated HTML and CSS files to [github_username].github.io repo

Once again make sure your inside [github_username].github.io directory in the terminal...

Now let’s host it!
```
git add .
git commit -m "Hosting my first Hugo website!"
git push origin main
```

Now go and check the [github_username].github.io repo

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/twa5ou9h0acpv1liqq68.png)

you will see Github pages in the repo, click that

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/m4a3edu5ftuyfp49h0ek.png)

If your deployment didn't show up wait for a couple of minutes and reload the same.

Finally, we hosted our first Hugo site 🥳 

<img width="100%" style="width:100%" src="https://i.giphy.com/media/l4RouGMf2234nMSCU9/giphy.gif">


Feel free to check out 👉🏻 [my portfolio](https://yeganathan18.github.io) 👈🏻

Do Like 👍 and follow for more interesting blogs 👨🏻‍💻
Comment you're valuable feedbacks down ✌️