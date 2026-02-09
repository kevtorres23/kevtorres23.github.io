---
title: HWS | Backend Documentation
date: 2026-02-08 02:55:00 -500
categories: [Hemisferios' Web System]
tags: [backend,ui,mongodb,express,react,node]
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

## Conventional folder structure
Before continuing, let's organize our backend directory by creating different sub-folders that help us organize our code more efficiently. The following is a conventional, recommended way to structure our backend:

```
- backend
    - src
        - controllers
        - routes
        - server.js
```

**Note**: After creating this new folder arrangement, it is necessary to update the ```package.json``` file to indicate the location that the ```server.js``` file will have once we create it, as it follows:

```javascript
"main": "src/server.js",
"scripts": {
    "dev": "nodemon src/server.js",
    "start": "node src/server.js",
},
```

It is important to notice that the ```dev``` script has the ```nodemon``` keyword before the route of the```server.js``` file. It was added to indicate that we want to **run our development server with Nodemon**, so that the functionality of this module is actually implemented (automatically refresh our server every time that changes are detected).

## Initialization of the ```server.js``` file
By convention, the ```server.js``` file in the backend directory of a MERN project is used to initialize our server connection to a specific port using Express. Just created, it looks like this:

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

From here, the following steps are creating our routes and controllers to let the client interact with the server dynamically in our application. In the following sections, I'll explain how I achieved this.

## Routes
A route can be understood as a **URL contained in an HTTP method that allows the client to perform different tasks, requests, and actions**. In Express, routes are defined with the ```Router()``` function.

The *routes* folder, within the *src* directory, is the place where we'll save our route configuration files.

The following are the route files I created and their purpose for the project:

- ```appointmentRoutes.js```
- ```contactMessageRoutes.js```
- ```patientRoutes.js```
- ```therapistRoutes.js```

## Controllers
A controller can be defined as a function that we create and that we can call in different locations or contexts in our project. In simple words, **they get a request, consult the logic to know what to do with it, and finally return a response**.

The *controllers* folder, within the *src* directory, is the place where we'll save our controllers. The following are the controller files I created for the project:

- ```appointmentControllers.js```
- ```contactMessageControllers.js```
- ```patientControllers.js```
- ```therapistControllers.js```

## Interaction between routes and controllers
The main purpose of separating our routes from our controllers, is to make our code more maintainable and optimal. To make them interact with each other, we need to **include the controllers within the routes**, as it follows, in the ```appointmentRoutes.js```:

```javascript
import express from "express";
import { getAllAppointments, createAppointment, updateAppointment, deleteAppointment } from "../controllers/appointmentControllers.js";

const router = express.Router();

// Route definition.

router.get("/", getAllAppointments);

router.post("/", createAppointment);

router.put("/:id", updateAppointment);

router.delete("/:id", deleteAppointment);

export default router;
```

Here, we first import the Express module and the controller files from their location in the directory. Then, we include them in the parameters of the router's HTTP method parameters.

## Universal routes with `app.use()`
Write how is `app.use("/api/appointments/", appointmentRoutes);` used to make it possible to improve the maintainabilty of the route declaration.

## Database configuration
One of the most important aspects of the backend functionality is.

## Configuration of `.env`
A .env file contains the

## Final files