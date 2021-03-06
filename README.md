
Vimogen is a simple cli tool to install, update and remove <a href="http://www.vim.org/>Vim</a> plugins. It can also help you keep plugins synchronized across multiple vim installations.

It requires no configuration (just a manifest file). Vimogen uses <a href="https://github.com/tpope/vim-pathogen/">Pathogen</a>, which lets you store all of your plugins in one place as git checkouts.

Motivation: Many plugins I use (vim-rails, syntastic, etc) get updated a lot and I wanted an easy way to keep my copies updated. I also wanted a better way to install all my favorite plugins whenever I install a new operating system. The alternatives either didn't use git or required configuration and other stuff I didn't like. 

With Vimogen, you can use the same `.vimrc` across multiple machines but have separate manifest files for each machine. This is useful if you don't want to use development plugins on a production machine, and so on.

Don't worry, finding Git URLs for all of your plugins is actually very easy 
because vim.org mirrors them all on github <a href="https://github.com/vim-scripts">here</a>.
You can also use bitbucket or any other git repository location if you need to.

Requirements
============
* A Unix-like system (Linux, OS X, etc.) and Git.
* The [Pathogen](https://github.com/tpope/vim-pathogen/ "Pathogen") plugin for Vim.

Installation
============
Create a manifest file called $HOME/.vimogen_repos that consists
of just git repositories. I supplied a sample .vimogen_repos file
which contains the plugins that I may use. Make up your own, though.

Vimogen auto-generates `$HOME/.vimogen_repos` if you run it
without creating the file first. It generates based off the
current Pathogen bundles you already have. This allows you to
update or uninstall any existing plugins you have. You'll only need
to edit .vimogen_repos yourself when you want to add more plugins.

Then run:

    git clone https://github.com/rkulla/vimogen.git
    chmod u+x vimogen.sh
    cp vimogen.sh ~/bin/vimogen 
    
or put it somewhere else in your $PATH if you don't use ~/bin.

Usage
=====
With Vimogen, you create a manifest file called `~/.vimogen_repos`
(or let vimogen generate one for you) and put Git clone URLs to Vim plug-in
repositories inside of it -- one line at a time -- like:
    
    https://github.com/tpope/vim-sensible.git
    https://github.com/tpope/vim-surround.git
    https://github.com/scrooloose/nerdtree.git
    https://github.com/tomasr/molokai.git
    ...

<a href="https://github.com/vim-scripts">Find vim URLs here</a>.

Run vimogen without arguments:

    $ vimogen

or, for more verbose output:

    $ vimogen -v

It will give you a menu of items to choose from:

    1) INSTALL
    2) UNINSTALL
    3) UPDATE
    4) EXIT
    Enter the number of the menu option to perform:

For example, typing `1` will install all the plugins listed in .vimogen_repos.

*    Choosing __INSTALL__ clones all the repos from .vimogen_repos into your Pathogen dir (~/.vim/bundle).
Skipping ones that already exist. 

Note: You can append new plugin repos to the .vimogen_repos file later and install them incrementally by re-running Vimogen's install command.

*    Choosing __UNINSTALL__ gives you a list of all your plugins:

         1) BACK                  8) tabular             15) vimogen
         2) ALL                   9) taglist             16) vim-pathogen
         3) ctrlp                10) tComment            17) vim-rails
         4) molokai              11) tlib_vim            18) vim-repeat
         5) pydiction            12) vcscommand          19) vim-snipmate
         6) python-mode          13) vim-addon-mw-utils  20) vim-surround
         7) snipmate-snippets    14) vim-jade            21) ZenCoding
         Enter the number of the plugin you wish to uninstall:

Press 1 to cancel. 2 to remove all your plugins at once.
    
*    Choosing __UPDATE__ runs a `git pull` on all of your bundles. 

TIP: If you ever want to temporarily disable a plugin, just use vimogen to UNINSTALL it, 
then whenever you want it back just run vimogen's INSTALL again.

TIP: Keep a reference to the vimogen repository in .vimogen_repos and it will show you
if a new version was updated whenever you run the update command. Then all you have to do is
copy the updated vimogen.sh file to your PATH to have the latest version. Do the same for
vim-pathogen.

FAQ
===
__Q: Can Vimogen install Vim color schemes, like Molokai?__

A: Yes. Anything that works with Pathogen (which is almost everything)
will work with Vimogen.

__Q: I downloaded a Vim plugin as a .zip file. What should I do?__

A: Vimogen doesn't use zip files, it uses git repos. All of
the plugins from vim.org are mirrored on https://github.com/vim-scripts so
find it on there and put its github clone URL into ~/.vimogen_repos. If
a plugin you want is not mirrored, it's probably still somewhere on github
or somewhere if you search.

__Q: I already use Dropbox (or similar) to keep my .vim/ directory synchronized. 
Why should I use Vimogen?__

A: Even if you've created a symlink from ~/.vim/ to ~/Dropbox/path/to/.vim/, that
will only help you keep your existing versions of plugins synchronized. Vimogen 
allows you to also automatically pull from all your plugins' git repos keep up-to-date.

License
=======
Copyright (c) Ryan Kulla. Distributed under the same terms as Vim itself. See :help license
