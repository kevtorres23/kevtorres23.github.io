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

The following are the route files I created:

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

## Route maintainability with `app.use()`
Since this project relies mainly on four main schemas or objects (appointments, patients, therapists, and contact messages), we'll need to specify the route that should meet each one of them.

With the ```app.use()``` function, we can declare the path of the routes only once in the ```server.js``` file by doing the following:

- First, **import the router of a schema in the ```server.js``` file**. 
 
    The router of a schema is defined in the route file of that schema (see how we wrote `export default router` in the previous section [Interaction between routes and controlles](#interaction-between-routes-and-controllers), to export the router of the appointment schemas, defined in the ```appointmentRoutes.js``` file.)

- Then, **add the imported router in the ```app.use()``` function** as its second parameter.

    In this method, the ```app.use()``` function receives two parameters: the first one is the route path for the schema, and the second one is the router that manages that schema.

With this method, each route declared in the route file of the schema will know which path to take. Refer to the following route:

`router.get("/", getAllAppointments);`

We no longer have to write ```/api/appointments/``` for each route in the route file of the schema because it is already declared in ```app.use("/api/appointments")``` in the ```server.js``` file. Therefore, we have the following route declarations in this last file:

1. For the **Appointment** schema: ```app.use("/api/appointments", appointmentRoutes);```
2. 

## First update of the ```server.js``` file
So far, we should have the following code in our ```server.js``` file:

```javascript
import express from "express";
import appointmentRoutes from "./routes/appointmentRoutes.js";

const app = express();

app.use("/api/appointments/", appointmentRoutes); // Added the route maintainability for the Appointment schema.

app.listen(5001, () => {
    console.log("Server started on PORT: 5001")
});
```


## Database configuration
From this point on, we can proceed to configure our database in MongoDB to start defining our schemas with Mongoose, which would allow us to finally start working with data in our project.

The following are the steps I followed to configure a database in MongoDB:

1. **Download and install** [MongoDB Community](https://www.mongodb.com/try/download/community) (the free, open-source MongoDB edition for developers).
2. **Create an account** or **log in** in the [MongoDB's official website](https://www.mongodb.com/).
3. **Create a new project** and initialize it with a free Cluster.
4. Retrieve the database **user credentials** (used to authenticate our connection to the database).
5. Retrieve the **connection string** (used to perform the connection to the database from our project's code).

## Configuration of `.env`
A ```.env``` file contains the global variables that we'll use in our project to perform backend-related actions, such as connecting to a local port and connecting to the database with the previously retrieved connection string.

Let's create this file within the main backend folder, out of any subdirectory, so that we have the following structure.

```
- backend
    - src
        - controllers
        - routes
        - server.js
    - .env
```

In the ```.env``` file, let's create the following global variables:

```javascript
PORT=5001
MONGO_URI=<connection_string>
```

Where the connection string is the one we retrieved previously when we were configuring our database (see the [Database configuration section](#database-configuration)). No we've defined these global variables, we can use them anywhere in our backend files by doing the following:

- Importing dotenv (```import dotenv from "dotenv"```) in the file.
- Calling the ```dotenv.config()``` function.
- Using the global variable as ```process.env.VARIABLE_NAME```.

See how I used the global ```PORT``` and ```MONGO_URI``` variables in different files in the following sections.

## Second update of the ```server.js``` file
So far, we should have the following code in our ```server.js``` file:

```javascript
import mongoose from "mongoose";
import express from "express";
import dotenv from "dotenv";
import cors from "cors";
import colors from "colors";
import appointmentRoutes from "./routes/appointmentRoutes.js";
import { connectDB } from "../config/db.js";

dotenv.config();
const app = express();

// Calling the connection method.
connectDB();

app.use("/api/appointments", appointmentRoutes);
// We'll add here the rest of the routes, such as contact messages, clients, therapists, etc...

app.use(cors());

// Using the global variable 'PORT'.
app.listen(process.env.PORT, () => {
    console.log(`Server started on PORT: 5001`.green)
});
```

## The ```db.js``` file
Let's create a new subfolder in our directory and name it as "config". Within it, we create the ```db.js``` file, intended to perform the connection to our MongoDB database.

```javascript
import mongoose from 'mongoose';
import dotenv from "dotenv";
import colors from "colors";

dotenv.config();

export const connectDB = async () => {
    try {
        await mongoose.connect(process.env.MONGO_URI);

        console.log(Successful conection to the database..blue);
    } catch (error) {
        console.error(Error connecting to MongoDB.red, error);
        console.log(process.env.MONGOURL);
    }
}
```

See how we used the ```MONGO_URI``` global variable in the line number 9, which contains the connection string needed to succesfully connect to our database.

If the connection fails, the error will be printed so that we can know the reason why it failed and address it.