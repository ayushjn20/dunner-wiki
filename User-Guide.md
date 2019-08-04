# Getting started

This document describes the usage instructions of the current stable version of Dunner.

1. Install Dunner by following one of the methods present in the [Installation Guide](https://github.com/leopardslab/dunner/wiki/Installation-Guide).

2. Run `dunner init` from command-line and it initializes current directory with a sample dunner task file. 
Or you can create a YAML file `.dunner.yaml` in your project directory.
It could look like as follows, 
    ```yaml
    publish:
      - image: node
        commands:
          - ["node", "--version"]
      - image: node
        commands:
          - ["npm", "install"]
      - image: mvn
        commands:
          - ["mvn", "package"]
    ```
    Have a look at [__How to write a Dunner file?__](#how-to-write-a-dunner-file) to know about more complex examples of creating tasks for Dunner.

1. Now you can run a task with Dunner as follows,
    ```bash
    $ dunner do publish
    ```
    **NOTE**: If you have created a YAML file with a different name, pass a flag `-t` with filename as the argument. Example,
    ```bash
    $ dunner do publish -t task.yml
    ```

**NOTE**: Your source code will be mounted to a directory called `/dunner` in the task containers and will be the working directory by default. If you want to change the working directory of the container, define it in the `dir` field of that corresponding step.

---


# How to write a Dunner file

## Step Fields Reference
Step fields are all the keys that are to be defined to describe a step of the tasks in the dunner file so that it can be parsed and interpreted by Dunner to execute certain commands inside a docker container.

|    Field   | Description                                                                                                                                                                       |
|:----------:|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `name`   | Name of the step that is being run here. It can be any alphanumeric string that is used for identification purpose only.                                                          |
|   `image`  | Image name or repository digest that has to be pulled from a registry. It is same as the first argument passed to the `docker pull ` command while pulling an image.              |
| `commands` | List of commands that has to be run inside the container built from the mentioned image or repository.                                                                            |
|   `envs`   | List of environment variables and their corresponding values that has to be exported inside the container.                                                                        |
|    `dir`   | To define the default working directory of dunner container where the current directory will be mounted. If no value is passed, working directory is set as `/dunner` by default. |
|  `mounts`  | List of directories that are to be mounted on the container.                                                                                                                      |
|  `follow`  | Name of some other task that has to be executed as step for this task.                                                                                                            |
|   `args`   | List of arguments to be passed to the task mentioned in the 'follow' field, which otherwise are passed through the command-line interface.                                        |


## Multiple commands
Since each step of the task is being executed inside the a different container, it is possible to run multiple commands inside a single step if there is a case of dependency of subsequent commands.

**Example**:
```yaml
build:
  - name: Setup
    image: node:latest
    commands:
      - ["npm", "--version"]
      - ["npm", "install"]
```


## Mounting external directories
It should be noted that there are two permission levels on which a directory can be mounted, viz., _Read-Only_ and _Read-Write_. The syntax for a directory mount is `<src>:<dest>:<mode>`. Where `<src>` is the path of directory present on the host; `<dest>` is the _absolute_ path where the directory has to be mounted on the container; `<mode>` is either **`r`** or **`w`** for _Read-Only_ and _Read-Write_ permission level, respectively.

**Example**:
```yaml
build:
  - name: Hosting
    image: php:apache
    commands:
      - ["service", "apache2", "restart"]
    mounts:
      - ~/project/backend/src:/var/www:r
      - ~/project/media:/var/www/media:w
```


## Exporting environment variables
Environment variables need to be explicitly defined which are to be exported in the containers. Those can also be fetched from host environment variables, or values can be defined in the `.env` file. More in [Dotenv file](#dotenv-file) section.

**Example**:
```yaml
static:
  - name: handle_static
    image: python3
    commands:
      - ["django-admin", "collectstatic"]
    envs:
      - DJANGO_SETTINGS_MODULE=mysite.settings
```


## Passing arguments through cli
Sometimes, there are cases where some arguments are required to be chosen at time of commencing the task. It is a desirable feature to choose those arguments at the time of running the `do` command.

**Example**:
```yaml
build:
  - name: make
    image: java
    commands:
      - ["make", "-j$1"]
```
```bash
$ dunner do build 8
```


## Use a task as a step for another task
There might be some incidents where a task is required to be run as a part of another task as some step. Dunner supports configuring the task file, i.e. the default `.dunner.yaml`, such that another task can be subsequently followed in a step of the original task.

**Example**:
```yaml
install:
  - follow: build
    args:
    - 8
build:
  - name: make
    image: java
    commands:
      - ["make", "-j$1"]
```


## Validating the dunner file
It is always convenient to have a validation check of the dunner file before executing the commands. While writing the dunner file, an user can validate the file for any syntax errors that might be fail the execution of the task. Use the following command on the CLI to validate the dunner file (default `dunner.yaml`).

```bash
$ dunner validate
```
---


# Advanced Usage

## Validation

You can validate your dunner task file without actually executing any task. 
```
dunner validate
```
Running above command from cli will list down any parse errors and validation errors in dunner configuration. 

## Dotenv file
Dunner has the facility to define certain environment variables in a separate environment file. This enables users to keep certain secrets like API keys, access tokens, passwords, etc. outside of the dunner file. Also, it can serve as a constants file too, making it a little less messier to change some parameters of the commands that are to be run through the dunner file. Dunner reads the filename (`.env`) by default, but a custom environment file with a different name can be chosen with `--env-file` flag. These variables can be invoked as explained [here](#exporting-environment-variables).

**Example of an environment file**:
```yaml
# .env
AWS_KEY='<YOUR_AWS_API_KEY>'
FIREBASE_KEY='<YOUR_FIREBASE_API_KEY>'
SSH_KEY_GITLAB='<YOUR_GITLAB_SSH_KEY>'
```


## Asynchronous mode
Concurrent execution of steps of task is quite a useful feature to reduce the total execution time, provided that there is no sharing of resources simultaneously among all the steps. This can be triggered with the `--async`/`-A` flag in the command line.

```bash
$ dunner do --async build
```


## Dry-run
This mode executes all the functions normally, except for the final execution of commands. Those functions include parsing the YML file, validating the syntax, connecting with Docker Hub and pulling docker images if required, building the containers and attaching the volumes. Thus, it can be checked that everything will work fine provided that the commands are correct. To execute a dry-run, use `--dry-run` flag as follows,

```bash
$ dunner do --dry-run build
```


## Verbose mode
Verbose mode provides more information on the terminal screen about what is going on during the execution. To enable a verbose output, use `--verbose`/`-v` flag as follows,

```bash
$ dunner do --verbose build
```