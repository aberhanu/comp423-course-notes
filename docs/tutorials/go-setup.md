# Setting up a dev container for Go

* Primary author: [Abiye Berhanu](https://github.com/aberhanu)

* Reviewer: [Ben Edwards](https://github.com/bkedwards)

## Prerequisites
1. `GitHub`: If you haven't set up a GitHub account, sign up at [GitHub](https://github.com/).
2. `Git`: Install Git [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
3. `Visual Studio Code`: Download VS Code [here](https://code.visualstudio.com/).
4. `Docker`: Install [Docker](https://www.docker.com/products/docker-desktop/) so you can run the dev container.

## Project Setup
### Set up a Directory and initialize Git:
1. Open your command prompt or terminal.
2. Create a new empty directory to host your project (Navigate to a different directory to change the location of the project to your preference)
```bash
mkdir Hello-Go
cd Hello-Go
```
3. Initialize a new Git repository:
```bash
git init
```
4. Create a README file and make a commit:
```bash
echo "# COMP423 Course Notes" > README.md
git add README.md
git commit -m "Initial commit with README"
```
### Set up a Remote Repository:
1. Log into your github account and head to the [Create a New Repository](https://github.com/new) page.
2. Include the following information:
    - Repository Name: Hello-Go
    - Description: "Initial Go project."
    - Visibility: Public
3. Omit setting up the repository with a README, .gitignore, or license.
### Link your Local Repo to GitHub:
1. Add the GitHub repository as your remote:
```bash
git remote add origin https://github.com/<your-username>/Hello-Go.git
```
Make sure to replace <your-username> with your github username.
2. Check your default branch name:
    - To do so run this command:
        ```bash
            git branch
        ```
        - If your default branch name isn't main, then rename it to main by running this subcommand:
            ```bash
            git branch -M main
            ```
-- Admonition: Old versions of git choose the name master for the primary branch, but these days main is the standard primary branch name.
3. Push your local commits to the GitHub repo:
```bash
git push --set-upstream origin main
```
4. If you refresh your web browser then you should see your local commit has been pushed to the remote repo.
### Set up a Development (Dev) Container
#### Add Development Container Configuration
1. Open the `HelloGo` directory in VS Code. You can do this via: File > Open Folder.
2. Install the Dev Containers extension for VS Code.
    - Go to the extensions Tab and search for the Dev Container extension (By Microsoft)
3. Create a `.devcontainer` directory in the root of your project
--Admonition The . at the beginning of the directory name/file indicates that it is a hidden configuration directory/file.
4. Within the `.devcontainer` directory create a `devcontainer.json` file.
    -  In this file we will specify the configuration for our dev environment as so:
```json
{
    "name": "Hello Go",
    "image": "mcr.microsoft.com/vscode/devcontainers/go:latest",
    "customizations": {
      "vscode": {
        "settings": {},
        "extensions": ["golang.go"]
      }
    }
}
```
--Admoniiton(Whole thingy): This configuration:
    - Uses the **Microsoft Go Dev Container image**.
    - Automatically installs the **Go VS Code plugin** (`golang.go`).
    - Runs the `postCreateCommand` to install Python dependencies if needed (optional).
#### Reopen our folder in a dev container:
1. Open Command Palette:
    - Mac Users: Press `Cmd+Shift+P`
    - Windows Users: Press `Ctrl+Shift+P`
2. Type "Dev Containers: Reopen in Container," and selecting the option.
    - This might take a moment as the image downloads
3. When the dev container setup is complete, close the current terminal tab, and open a new terminal pane within VS Code
4. Try run: 
 ```bash
 go version 
 ``` 
*If you check, you can see that you are currently running the latest version of go.*
## Lets Code!
### Hello COMP423 Program
We are now ready to write our first Go Program.

1. Enable Dependency Tracking:
    - In your dev container run the go mod init comand like so:
```Go
go mod init example/hello
```
2. In VS Code create a `hello.go` file, this is where we will be writign our program.

3. In the `hello.go` file write this code:

```Go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

- In first line `package main`: we create the main package. 
    - Packages are a way to group functions and they are made up of all the files within the same directory.
- Next with `import "fmt"`: we import the fmt package wich is a popular package from the standard library packages. 
    - The fmt package has functions for formatting text, including printing to the console. 
- Finally we implement a main function to print a message to the console. 
    - A main function executes by default when you run the main package.

4. Run your Program:
    - To see your greating, us the go run command:
```bash
go run .
```


### Building and Running an Executable (Go Build) 

While the go run command is a useful shortcut for compiling and running a program when you're making frequent changes, it doesn't generate a binary executable.

- The go build command compiles the packages, as well as their dependencies, however it doesn't actually install the results.

From the command line in the hello directory, run the go build command to compile the code into an executable.

```bash
go build
```
Finally, run the new hello executable to confirm that the code works.
```bash
./hello
```
--Admonition: The `go build` command is used to compile Go code into an executable binary. This is much like how gcc would compile a C program into a runnable file. In contrast, go run, only compiles and runs the code in memory, go build writes out a fully independent binary, which then can be executed directly via./binary-name, thus reusable and portable.

## Congrats
You succesfully built your first Go program, Cheers to many more!
