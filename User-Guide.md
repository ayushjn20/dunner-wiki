1. Install Dunner by compiling the source code on your machine. Read the [Installation Guide].(https://github.com/leopardslab/Dunner/wiki/Installation-Guide)

( We will be adding more methods like RPM & Deb packages in the future )

2. Create a file called `.dunner.yaml` in your project directory.
It could look like as follows, 

```
publish:
    - image: node
      command: ["node", "--version"]
    - image: node
      command: ["npm", "install"]
    - image: mvn
      command: ["mvn", "package"]
    - image: mvn
      command: ["mvn", "package"]
```

3. Now you can run a task with Dunner as follows,

`Dunner do publish`

**NOTE**: Your source code will be mounte to a directory called `/dunner` in the task containers and will be the working directory by default.