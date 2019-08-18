To start creating our project we need to do the following steps:

- Install yarn
- Create a React App

**What is `yarn`?**
Yarn is a `JavaScript` package manager and task runner:

- Install yarn using the following command
  ```shell
  $ brew install yarn
  ```
  This command will install yarn globally on your device

Now you have two options to either 1) clone our starter file to get our starting components or 2) you can create your project from scratch (recommended so that you get used to it).

**How to clone the starter file? (option 1)**

- Go to the project's [repo](https://github.com/grumpy13/TrackMyShows_ReactJS)
- Fork the project to your github account
- Copy the url and go to your terminal/shell

```shell
$ git clone <your url here>
```

```shell
$ cd <the project's name>
```

```shell
$ yarn install
```

this will install the same version of any libraries we have installed in this project

**How to create a `React App`? (option 2)**

- Using the terminal go to the location on your device where you want to create the project
- then using the following command

  ```shell
   yarn create react-app track-my-shows
  ```

  this will create a folder that will contain your project files

**How to run the project?**

- To run your project and see the changes you make live in your browser use the following commands
  ```shell
  cd track-my-shows
  yarn start
  ```
  The first command will take you to the project's folder
  The second command will run your project
