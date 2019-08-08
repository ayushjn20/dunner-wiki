We'd love it if you can help us develop Dunner and we are glad you thought of reading this developer guide before contributing!

Before working on a pull request please let us know by creating or commenting on an issue on [GitHub](https://github.com/leopardslab/dunner/issues), and we'd also love to hear from you in our [community channel](https://gitter.im/LeaopardLabs/Dunner).

# How can you help us?

* You can report any issues you found on [Github](https://github.com/leopardslab/dunner/issues)
* Help us improve our [Documentation](https://github.com/leopardslab/dunner/wiki)
* Write Dunner recipes that can help others and send us PR on [Dunner Cookbook](https://github.com/leopardslab/dunner-cookbook)
* Write a blog post on Dunner and it published on our channel
* Help someone get started with Dunner on our [discussion forum](https://gitter.im/LeaopardLabs/Dunner)
* Contribute Code to Dunner! Issues labelled `good first issue`, `help wanted` and `bug` are good to start with.

# Pull Requests
* Before creating a PR, always make sure there is a relevant issue for it. If not, create one yourself.
* Make sure to prefix the issue id in commit message titles like, `[#1] Mount the source code as a volume to containers` where the `#1` is the issue id.
* Make all the PRs to `develop` branch.
* Run `make precommit` locally before raising PR, this checks for standard Go code styles.

# Setup

`Makefile` is your friend! Have a look at all tasks defined [here](https://github.com/leopardslab/dunner/blob/master/Makefile).

* Install [dep](https://github.com/golang/dep) as described [here](https://github.com/golang/dep#installation)
* To install project dependencies, run `make setup`
* To build project, run `make build`
* To run unit tests, run `make test` 

