title: 'deploy hexo with "git push" (spoiler: git hooks are rad)'
date: 2015-04-16 04:39:59
tags: ["git", "clouds"]
---

Hello friends,

I generate my blog with [hexo](http://hexo.io/), my third or fourth blog generator so far, and I'm really enjoying it. Hexo is really flexible, has all sorts of convenience functions, and is *super* easy to deploy (it's literally just `hexo deploy`). Deploys were such a problem for me with my last blog generator that I didn't write a blog post for 6 months! (It was seriously like five steps, and it was super slow even *after* I automated it!)

So I'm super happy with `hexo deploy`. This is my workflow:

```
 $ {100 freaking git commands, someone seriously needs to write a usable wrapper for git}
 $ git push      # push to server
 $ hexo generate # generate static site
 $ hexo deploy   # copy static site to remote host
```

But can I do better? (Yes)

I will *always* run `hexo generate` and `hexo deploy` after `git push`. So why do I need to type them myself? I pay Amazon good money for Robot Computers in the Cloud™ (my buzzword game is on point), so let's put those robots to good use and set up a [git server-side hook](http://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks#Server-Side-Hooks) to generate and deploy the site for us.

# Git hooks

What are git hooks? Git hooks are scripts that you can tell git to run after certain events. There are [many different flavors](http://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) of git hooks, but we just need a server-side `post-receive` hook. (Btw, this won't work with GitHub. But that's okay, because setting up your own "private" GitHub is actually *way* easier than you probably think it is! As long as you have ssh access to a machine, you can create remote git repos on it. I'll write a post about that soon, but you can follow the [git book's slightly overcomplicated setup](http://git-scm.com/book/en/v2/Git-on-the-Server-Getting-Git-on-a-Server#Putting-the-Bare-Repository-on-a-Server) for now.)

A `post-receive` server-side git hook is a hook that runs on your server after a push. `git push` won't actually return until `post-receive` is finished running, so you can be sure that your site is completely generated/deployed after `git push` finishes.

# THE ACTUAL HOOK (the moment you've all been waiting for)

First, some setup.

```
# BEFORE YOU START: Make sure you have npm and node set up correctly on your
# server.
$ ssh <username>@<your-server> # log into your server
$ cd <git-repo-for-site>/hooks # assuming your repo is a bare repository
$ touch post-receive           # create post-receive
$ chmod +x post-receive        # hook must be executable
$ nano post-receive            # s/nano/your-favorite-text-editor/
```

And then paste this sucker in:
```
#!/bin/sh

# Hooks are executed with the top level git repository as their working
# directory, i.e. "/home/person/site", not "/home/person/site/hooks".

# This script assumes your remote repo is a "bare" repository, which it should
# be. More info:
# http://git-scm.com/book/en/v2/Git-on-the-Server-Getting-Git-on-a-Server

mkdir tmp # I'm 90% sure you can make arbitrary directories inside a git repo.
# check out the branch "master" into "tmp"
git --work-tree=tmp checkout master
# move to "tmp"
cd tmp
# install hexo modules into "tmp"
npm install
# generate your site (to "public" by default)
hexo generate
# copy your site (recursively, verbosely, preserving file metadata) from
# "public" to your website directory.
rsync -arv public/ <path-to-website, e.g. "~/www">
# clean up "tmp"
cd ..
rm -r tmp
```

(Make sure to change the path on the `rsync ...` line!)

And that's it! The robots are doing your bidding, and `git push` is all you need to share your awesome blog posts with the world! You should see the output of all of those commands whenever you `git push`. (If you run into issues with the git hook, double check that you made `post-receive` executable. If it's still broken, leave a comment.)

Now, there are some obvious ways to optimize this (like by installing the node modules globally once, instead of on every push), and I encourage you to optimize your own script yourself :D

happy hacking,
s
