---
title: Trouble setting up rubocop with Sublime
layout: post
date: 2018-10-15 02:44:26 +0530
description: Rubocop sublime not working?
---

Using Sublime Text 3, RVM and want to set up robocop?

Make sure you have installed rubocop in your default ruby version.
```
gem install rubocop
```

Open the command palette, press ctrl+shift+p (Win, Linux) or cmd+shift+p (OS X). Start by typing `Package Controll: Install Package`.

![Package Controll: Install Package](/public/images/posts/package-control-install-package.png)

Now search for the rubocop package. Just select the package and hit enter.

![Package Controll: Search Rubocop](/public/images/posts/rubocop-package-search.png)


Once installed you can see the package options in the tool bar

![Package Controll: Search Rubocop](/public/images/posts/rubocop-check-single-file.png)

Open any ruby file and run 'Rubocop Check Single File'

![Package Controll: Search Rubocop](/public/images/posts/rubocop-check-single-file-output.png)

## Troubleshoot

Sometimes after all the installation, you may see `/bin/sh: 1: /home/al/.rvm/bin/rvm-auto-ruby: not found`, sublime just cannot find your ruby path.

Lets find out the path first, go to console and run
```
al@al$ which rvm-auto-ruby
/usr/share/rvm/bin/rvm-auto-ruby
```

Open `Preferences > Package Settings > Rubocop > Settings - User` and add
```
{
  // The path to RVM's rvm-auto-ruby binary
  "rvm_auto_ruby_path":  "/usr/share/rvm/bin/rvm-auto-ruby"
}

```
Replace the path with the output of the `which rvm-auto-ruby` command.
