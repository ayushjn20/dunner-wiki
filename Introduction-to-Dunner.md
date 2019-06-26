# Dunner
> The Docker Task Runner

## Why use a task runner?
Task runner will speed up the development process by making everything automated. Performing repetitive tasks like compilation, unit testing, deployment, release automation, application setup become easy. It also lets you share the tasks with your team.

## What is Dunner?
Dunner is an open-source task runner based on Docker, simple and flexible. Define docker tasks, configure the environment, and that’s it!

Just create a `.dunner.yaml` file as below:

```yml
release:
  - image: golang
    commands:
      - [“make”, “build”]
  - image: goreleaser/goreleaser
    commands:
      - [“echo”, “Running the release script”]
      - [“goreleaser”, “release”]

```

Running `dunner do release` from command-line will now run the release task inside a Docker container. It runs the build command using `golang` image and then runs release script using `ubuntu:latest` image in another container.

## Why use Dunner?
* Automate repeated tasks of spinning up a container, running commands and closing it
* Easy configuration
* Define your docker tasks once and forget attention to detail every time
* Share tasks with your team
* Run tasks using multiple images faster and fully automated!
* Simple usage and easy installation for all platforms

## Here’s a preview!

[Screencast of Dunner install and run sample dunner file]

## Installation
Based on your OS and machine architecture, Dunner can be installed in many ways. 

[All install options with instructions]

### Test your installation

Run `dunner --help` on command-line and it should display usage and available commands.

