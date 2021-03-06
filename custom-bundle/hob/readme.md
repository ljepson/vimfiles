
hob.vim
=======

**Hob is like Hub, except that it has an `o` in the middle of it**

Hob is your Github Vim buddy, it doesn't do much.

There's only one feature: A simple wrapper to `:r!` command.

See `:h r!`

> Execute {cmd} and insert its standard output below the cursor or the specified
line.  A temporary file is used to store the output of the command which is
then read into the buffer.  'shellredir' is used to save the output of the
command, which can be set to include stderr or not.  {cmd} is executed like
with ":!{cmd}", any '!' is replaced with the previous command |:!|.

So I tried this:

```
:r! curl -s https://raw.github.com/h5bp/html5-boilerplate/master/index.html
```

It worked, it fetched the latest version of h5bp's `index.html` and inserted
the output below my cursor. that's awesome.

And then I tried this:

```
:r! curl -s https://raw.github.com/cloudhead/hijs/master/hijs.js | uglifyjs
```

It worked too! The [hijs](https://raw.github.com/cloudhead/hijs/master/hijs.js)
script is piped through uglifyjs before being inserted below my cursor. That's
awesome.

And then, I wanted to type less characters.

Commands
--------

### HobGet

`:HobGet <user/repo> <file>`

is a simple command to fetch and insert below the cursor or the specified line
a filename from a Github repository.

`:HobGet` is pretty dumb right now, but It might get clever with some amount of
completion on user/repo and filenames (via github api, will need some sort of
caching system)

Predefined URLs may be defined and added with the `hob#define(id, url)`
function.

```
:call hob#define('blah', 'http://example.com/path/to/blah.blah')
```

When defined this way, URLs may point to anything (not necessarily
within a github repo) and `:HobGet blah` becomes a valid command.

Otherwise, information about github user, repository and filepath in the
form of `:HobGet user/repo path/to/filename.ext` must be used.

### HobHelp

`:HobHelp`

Nothing fancy, is similar to `:h hob`

Configuration
-------------

`:HobGet foo` is a valid command assuming `foo` identifier was defined
through `g:hob_urls` in your `.vimrc` (or via `hob#define` at runtime)

```vim
"
" Hob config
"
" A dictionnary with key / value pairs where key is the id, and value is the
" remote url

let g:hob_urls = {}
let g:hob_urls['h5bp-css'] = 'https://raw.github.com/h5bp/html5-boilerplate/master/css/style.css'
let g:hob_urls['h5bp'] = 'https://raw.github.com/h5bp/html5-boilerplate/master/index.html'
```

Limited amount of completion is supported, which is only on predefined URLs
right now.

Install
-------

*once in its own repo, the following would apply. For now, simply git clone
the repo locally, and copy this directory (vim/vim/bundle/hob.vim) in one of
your runtimepath*

---

If you don't have a preferred installation method, I recommend
installing [pathogen.vim](https://github.com/tpope/vim-pathogen), and
then simply copy and paste:

    cd ~/.vim/bundle
    git clone git://github.com/mklabs/vim-hob.git

Once help tags have been generated, you can view the manual with
`:help hob`



License & Acknowledgement
-------------------------

Add credits here

License: Same as the three plugins mentioned above, same as Vim. See
`:help license`.


