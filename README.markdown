Introduction
-------------

This is a set of directions and files for setting up a new Ubuntu box just the way I like it.  Fork and modify as you see fit!

Pre-requisites
---------------

* Ubuntu 10.04 install
* Working internet connection

Install Ubuntu Packages
-------------------------

I install a basic set of packages on all my Ubuntu development boxes.

    sudo aptitude install build-essential bison openssl libreadline5 libreadline-dev curl git-core zlib1g zlib1g-dev libssl-dev vim libsqlite3-0 libsqlite3-dev sqlite3 libreadline-dev libxml2-dev git-core subversion autoconf vim-gnome vim-ruby

Install Ruby
-------------

I use RVM to manage my ruby versions.  To install RVM do:

    bash < <( curl http://rvm.beginrescueend.com/releases/rvm-install-head )

You need to replace the line in your ~/.bashrc that says:

    [ -z "$PS1" ] && return

with

    if [[ -n "$PS1" ]]; then

Now add this to the last line of the file

    if [[ -s $HOME/.rvm/scripts/rvm ]] ; then source $HOME/.rvm/scripts/rvm ; fi
    
    fi

I normally install ruby 1.9.2-head by default:

    rvm install 1.9.2-head

You can get a list of available rubies using:

    rvm list known

And see their install dependencies using:

    rvm notes

Configure Bash shell
---------------------

I prefer to use bash as my shell.

Paste the following to set my git status in the prompt:

    function parse_git_dirty {
      [[ $(git status 2> /dev/null | tail -n1) != "nothing to commit (working directory clean)" ]] && echo "*"
    }
    function parse_git_branch {
      git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e "s/* \(.*\)/[\1$(parse_git_dirty)]/"
    }


    # set a fancy prompt (non-color, unless we know we "want" color)
    case "$TERM" in
    xterm)
        PS1='\[\033[0;35m\]\w\[\033[0;36m\]$(parse_git_branch)\[\e[0m\]: '
        ;;
    *)
        PS1='\w$(parse_git_branch)\[\e[0m\]: '
        ;;
    esac

Conclusion
-----------

Voila!  Your done setting up this dev box!  I've also included samples of my .bashrc for reference.
