---
title: HWS | Backend Documentation
date: 2026-02-08 02:55:00 -500
categories: [Hemisferios' Web System]
tags: [react,ui,backend,express,mongodb,node,tailwindcss,shadcn]
published: true
---

## Introduction - About the project
The Hemisferios' Web System is a software project I had the opportunity to work on for my final internship program at the university. Here, I worked on a unified system that comprehends a website and an appointment system (for administrators only) for Hemisferios, a clinical center that offers language and communication therapy for children.


In this page, you can find the documentation for the backend functionality of the project, which contains an exhaustive explanation of the following elements:
* Installed dependencies.
* Setup of the backend environment, from start to finish.
* Creation and setup of the MongoDB's database.
* Schemas, modules, and endpoints for the client to consume.

## Environment setup
First and foremost, it is necessary to create a new Node.js application in a folder named "backend", in the very root of the project. Once within the folder, we open a terminal and we run the following command:

```bash
npm init -y
```

This will create the ```package.json``` file of our project, which contains essential information about it, such as its name, version, scripts, and execution commands.

Now, we can proceed to install all the necessary dependencies and modules that will be used to develop the backend of our project. The following is a list of the packages I installed:

- **Express**: a web framework used to agilize backend development with features like robust routing, HTTP helpers, and high performance.
  
```shell
npm install express
```

- **CORS**: it establishes response headers to define which origins can reed the responses of our server.
  
```shell
npm install cors
```

- **Nodemon**: it updates the Node server every time changes are detected, so that we no longer have to do it manually by inserting commands in the terminal.
  
```shell
npm install nodemon
```

- **Mongoose**: a MongoDB object modeling tool that is mainly used to add validations to the created schemas.
  
```shell
npm install mongoose
```

- **Dotenv**: it allows to dynamically inject variables from a ```.env``` file into ```process.env```.
  
```shell
npm install dotenv
```

- **Colors**: it allows to add customizable colors and text styling to the terminal messages of the Node server.

```shell
npm install colors
```

I used this particular set of modules based on my personal preferences, but any other dependencies that could be useful in the backend development process can be incorporated into the environment if needed.

## Initialization of the ```server.js``` file
By convention, the ```server.js``` file in the backend directory of a MERN project is used to initialize a server connection to a specific port using Express. Initially, my server.js file looked like this:

```javascript
import express from "express";

const app = express();

app.get("", (req, res) => {
    res.send("Hellooo")
});

app.listen(5001, () => {
    console.log("Server started on PORT: 5001")
});
```

Here, we initialize the connection to the port 5001 (in my case) using the Express module that we are importing at the start of the file.

**NOTE:** I manually changed the module importation type to be the *ES6* one (```import <moduleName> from <module>```). By default, the importation is set to be the *CommonsJS* type, but it can be changed by updating the following line in our ```package.json``` file, as it follows:

```javascript
"type": "module" // Set to ES6.
```
