# 1. Install by compiling the source code.

**Note**: You need 'Dep' to download the dependencies. See how to install Dep [here](https://golang.github.io/dep/docs/installation.html).

1. Do a `dep ensure` to download all the dependencies of Dunner.

2. Do `go install` to install Dunner on your machine.

Now you can use Dunner like `Dunner do sometask`


***

**Note:** We will be adding more methods like RPM & Deb packages in the future


# 2. Install via Brew on Mac OS X
[Dunner](https://github.com/leopardslab/Dunner) can be installed via [Homebrew](https://brew.sh/). On Mac OS X, you can install by running below command:

```
brew tap leopardslab/dunner
```
or
```
brew install leopardslab/homebrew-dunner/dunner
```

To reinstall, run `brew reinstall dunner`.
