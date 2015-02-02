nitrogen
=========

nitrogen is a simple, self-contained, dependency manager for Go.

It is a bash script made of less than 150 lines of code. Dependencies are 
listed in the same file of the dependency manager, so you need to distribute only 
one file and your users don't have to install other tools. Moreover, nitrogen 
leverages on the git and hg versioning systems, so you don't need to distribute 
the full dependecies tree with your package, the standard gopath mechanism just 
works well.

Warning
--------

I consider nitrogen in beta, so expect bugs. Don't use it in a production 
environment!

Set up dependencies
--------------------

Dependencies are listed as comments starting with '#@'. Dependencies are
formatted as "package vcs version", where "package" is the name of the Go
package that you need to install (e.g "golang.org/x/crypto/blowfish"),
"vcs" is the version controll system of the package (git or hg) and
"version" is every suitable option for `git checkout` or `hg update`.

e.g.
```bash
    #@ code.google.com/p/go-uuid hg -c 35bc42037350
    #@ golang.org/x/crypto git 4ed45ec682102c643324fae5dff8dab085b6c300
```

### Hey, I just want to freeze dependecies at the current version!

That's why nitrogen has a '-f' (--freeze) option.

```bash
    nitrogen -f
```

You should find your dependencies listed in the first lines of your nitrogen
file.

Install dependencies
---------------------

To install your package with the required dependencies, download it with
    
```bash
    go get -d PACKAGE
```

Then start nitrogen with '-i' (--install). 

```bash
    nitrogen -i
```

If you want to mantain your dependencies at the version required by your
package, instead launch it with '-i --no-clean'

```bash
    nitrogen -i --no-clean
```

After you have done with the work on your package, restore depencencies
at the default (master branch or latest version) versions with

```bash
    nitrogen -c
```

License
--------

nitrogen is released under [the MIT License](http://opensource.org/licenses/MIT).


