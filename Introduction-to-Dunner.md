# Dunner
> The Docker Task Runner

## Why use a task runner?
Task runner will speed up the development process by making everything automated. Performing repetitive tasks like compilation, unit testing, deployment, release automation, application setup become easy. It also lets you share the tasks with your team.

## What is Dunner?
Dunner is an open-source task runner based on Docker, simple and flexible. Define docker tasks, configure the environment, and that’s it!

Just create a `.dunner.yml` file as below:

```yml
release:
  image: ubuntu:latest
  name: dunner_release
  commands:
    - [“echo”, “Running the release script”]
  envs:
    - USER=`$USER_NAME`
    - API_KEY=`$RELEASE_API_KEY`
  mounts:
    - `$BUILD_DIR`:/app
```

Running `dunner do release` from command-line will now run the release task inside a Docker container, using `ubuntu:latest` image.

## Why use Dunner?
* Automate repeated tasks of spinning up a container, running commands and closing it
* Easy configuration
* Define your docker tasks once and forget attention to detail every time
* Share tasks with your team
* Simple usage and easy installation for all platforms

## Here’s a preview!

[Screencast of Dunner install and run sample dunner file]

## Installation
Based on your OS and machine architecture, Dunner can be installed in many ways. 

[All install options with instructions]

### Test your installation

Run `dunner --help` on command-line and it should display usage and available commands.

