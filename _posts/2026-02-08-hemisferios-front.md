---
title: HWS | Frontend Documentation
date: 2026-02-08 02:55:00 -500
categories: [Hemisferios' Web System]
tags: [react,ui,frontend,express,mongodb,node,tailwindcss,shadcn]
published: true
---

## Introduction - About the Project
The Hemisferios' Web System is a software project I had the opportunity to work on for my final internship program at the university. Here, I worked on a unified system that comprehends a website and an appointment system (for administrators only) for Hemisferios, a clinical center that offers language and communication therapy for children.

In this page, you'll find the processes, methods and functions used to build the **frontend** of the project. I'll explain the following:

- Installed dependencies.
- File organization.
- Explanation of modules and functions.
- Endpoint consumption.
- UI/UX decisions.

The following is the tech stack I used: 
* Next.js.
* React.
* Tailwind CSS.
* Shadcn-UI.
* Axios.

## Environment Setup
Let's first create a folder named `frontend` in the root of our project's directory. We then access this new folder and run the following command in a terminal to create a new Next.js application.

```bash
npx create-next-app@latest app-name
```

In the terminal, we will be asked if we want to use the recommended Next.js defaults, which includes the following technologies:

- **TypeScript**: A typed programming language that builds on JavaScript.
- **ESLint**: A program that finds JavaScript code issues to ease their spot and fix.
- **Tailwind CSS**: A CSS framework for writing styles in the form of utility classes.
- **App Router**: A file-system based router from Next.js to allow navigation between pages.
- **Turbopack**: An incremental bundler for React Components and Typescript codebases.

I accepted to use these technologies in my project, but we can also customize our own settings.

To install **Shadcn-UI**, we run the following command:

```npx shadcn@latest init```

Then, we can start adding components to our project as it follows:

```npx shadcn@latest add <componentName>```

Refer to the [official documentation](https://ui.shadcn.com/docs/components) to see the components that can be installed.

## Folder Structure
Since this project contains two separated views, one for the **website**, accessible for all users, and one for the **appointment system**, accesible for administrators only, I was looking for a folder structure that allowed me to easily find and maintain the files that correspond to each view.

In the main ```frontend``` directory, there is a subfolder named ```app```, which is, conventionally, the place where we should create the folders for each page of our project, and their corresponding ```.tsx``` file. In my case, it looks as it follows:

```
- frontend
    - app
        - page.tsx (Homepage of the website)
        - about-us
            - page.tsx
        - book-appointment
            - page.tsx
        - contact
            - page.tsx
        - finished-appointment
            - page.tsx
        - services-and-prices
            - page.tsx
        - system
            - Folders for each page of the Appointment System.
```

The ```public``` folder in our main directory is the place where we can save images, illustrations, and SVG files that we intend to use in a page.

Then, I created two important folders: `website` and `system`, which each simultaneously contains the following subfolders:

- `components`: This subfolder saves TypeScript in JSX (`.tsx`) files that contain reusable code for UI elements, such as buttons, cards, inputs, badges, and containers.
- `modules`: This subfolder contains functions, class declarations, Zustand stores, and any other code that has one or more specific functionalities in our project, such as defining input validation methods, handling some data and returning it in a particular way, or detecting a UI section's visibility when it enters the viewport, for example.
- `sections`: This subdolfer contains `.tsx` files with the content of the sections of a whole page, such as the hero section, testimonials, contact form, etc.

They look like this:

```
- frontend
    - website
        - components
        - modules
        - sections
    - system
        - components
        - modules
        - sections
```

The objective of having these three subfolders for both the website and the appointment system of the project is to improve modularity and better organize the overall code and structure.

# Modules and Functions
In this section, I will explain the purpose and functioning of the modules that I created to achieve a specific task in specific components or UI sections.

## Website

### PDF Generation

### Classes

### Input Change Handling

### Managing the Center's Availability

### Zustand's Appointment Store

### Visibility Detector

## Appointment System