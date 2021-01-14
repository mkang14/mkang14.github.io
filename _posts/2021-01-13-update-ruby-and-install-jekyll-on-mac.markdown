---
layout: post
title:  "Update Ruby and Install Jekyll on Mac"
date:   2021-01-13 18:33:45 -0500
categories: jekyll update
---
I wanted to learn the syntax of a language other than [Python][python]. I came across [Ruby][ruby] while using [GitHub][github],
so decided to take a basic class on Ruby. As a first step, I checked my current version by opening terminal and running <code> ruby -v </code>.
I have a 2019 Macbook Air and it had 2.6.3.  

I found the following steps on GitHub and ran each step on the terminal to update to version 3.0.0 (released 2020-12-25).  

* <code> curl -sSL https://raw.githubusercontent.com/rvm/rvm/master/binscripts/rvm-installer | bash -s stable </code>  
_I had to restart the terminal after this first step._  
* <code> rvm list known </code>  
* <code> rvm install ruby@latest </code> _(this step took a while and the fan on my Mac was spinning at **full** speed)_  
* <code> ruby -v </code>  
_My version still showed 2.6.3, so I had to run one more line._  
* <code> rvm use ruby-3.0.0 --default </code>  
* <code> ruby -v </code>  
_And now the version shows as 3.0.0 - all done!_ :+1:  


Next I installed [Jekyll][jekyll-gh] since I want to use [GitHub Pages][github-pages] for blogging.
But I had issues in the process and had to dig around for a solution.  

Normally, you should be able to run this on the terminal to install:  
* <code> gem install jekyll bundler </code>  

Bundler was properly installed. However, for Jekyll, I kept getting an error saying:  
```shell
In file included from binder.cpp:20:
./project.h:119:10: fatal error: 'openssl/ssl.h' file not found
#include <openssl/ssl.h>
         ^~~~~~~~~~~~~~~
1 error generated.
make: *** [binder.o] Error 1

make failed, exit code 2
```

After trying a few things, including reinstalling openssl, what worked for me was adding some lines to my bash profile (I used [Atom][atom]).  
* <code> atom ~/.base_profile </code>  
I added this at the bottom of the profile and saved.  
```shell
LD_LIBRARY_PATH=/usr/local/opt/openssl/lib:"${LD_LIBRARY_PATH}"  
CPATH=/usr/local/opt/openssl/include:"${CPATH}"  
PKG_CONFIG_PATH=/usr/local/opt/openssl/lib/pkgconfig:"${PKG_CONFIG_PATH}"  
export LD_LIBRARY_PATH CPATH PKG_CONFIG_PATH
```  
* <code> source ~/.bash_profile </code>  
* <code> gem install jekyll </code>  
* <code> jekyll -v </code> to check if it was properly installed now.  
And now finally installed! :+1:

[python]:https://www.python.org/
[ruby]: https://www.ruby-lang.org/en/
[github]: https://github.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[github-pages]: https://pages.github.com/
[atom]: https://atom.io/
