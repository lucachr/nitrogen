nitrogen
=========

nitrogen is a simple dependency manager for Go.

It is a bash script made of less than 150 lines of code that you should 
distribute with your Go package. Nitrogen leverages on the git and hg 
versioning systems, so you don't need to distribute the full dependecies 
tree with your package, the standard gopath mechanism just works well. 

Warning
--------

I consider nitrogen in beta, so expect bugs. Don't use it in a production 
environment!

Set up dependencies
--------------------

Dependencies are listed in a file called 'deps' that is located in the 
same directory of nitrogen (i.e. your package root directory). Dependencies 
are formatted as "package version", where "package" is the name of the Go 
package that you need to install (e.g "golang.org/x/crypto/blowfish") and 
"version" is every suitable option for `git checkout` or `hg update`.

e.g.
```
    code.google.com/p/go-uuid -c 35bc42037350
    golang.org/x/crypto 4ed45ec682102c643324fae5dff8dab085b6c300
```

### Hey, I just want to freeze dependecies at the current version!

That's why nitrogen has a '-f' (--freeze) option.

```
    nitrogen -f
```

You should find your dependencies listed in the generated 'deps' file.

Install dependencies
---------------------

To install your package with the required dependencies, download it with
    
```
    go get -d PACKAGE
```

Then start nitrogen with '-i' (--install). 

```
    nitrogen -i
```

If you want to mantain your dependencies at the version required by your
package, instead launch it with '-i --no-clean'

```
    nitrogen -i --no-clean
```

After you have done with the work on your package, restore depencencies
at the default (master branch or latest version) versions with

```
    nitrogen -c
```

License
--------

nitrogen is released under [the MIT License](http://opensource.org/licenses/MIT).
