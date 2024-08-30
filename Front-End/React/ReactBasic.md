# Learning React: A Beginner's Guide

## What is React?

React is a JavaScript library for building user interfaces, primarily for single-page applications. It enables developers to create reusable UI components that can manage their state, making it easier to build complex interfaces efficiently.

### 0. **Single Page Application**
   - Single-Page Applications (SPAs) are a type of web application that load a single HTML page and dynamically update the content as the user interacts with the app. This contrasts with traditional multi-page applications, where each user interaction (like clicking a link) requires the browser to request a new page from the server.

### 1. **Composition Over Inheritance**
   - Unlike traditional object-oriented programming, which relies on inheritance, React uses composition. 

### 2. **Component-Based Architecture**
   - React encourages building UIs by breaking them down into small, self-contained components. Each component manages its own state and can be combined with other components to create complex interfaces.(AKA component oriented architecture)

### 3. **React vs. Angular**
   - While Angular is a full-fledged framework that provides an out-of-the-box solution for building web applications. React is a library primarily focus on building user interface. It doesn’t include features like routing, form handling, or state management out-of-the-box, which means you need to rely on additional libraries.


## React.js Overview

### 0. Understanding Single Page Application
- **Definition:** SPAs are web applications that load a single HTML page and dynamically update the content as the user interacts with the app. This differs from traditional multi-page applications, where each interaction requires the browser to request a new page from the server.
- **Efficiency:** SPAs are generally more efficient as they are avoid reloads. React also utilizing client side rendering which lightened workload for the server side. The bulk of the rendering happens in the browser using JavaScript, specifically React in this case. React takes over and manages the DOM on the client side.

## 1. Key Features of React Framework
- **Component-Based Architecture:** React components are broken the application down into smaller, reusable parts called components. Components in React are self-contained, meaning they include their own HTML, CSS, and JavaScript logic. 
- **Virtual DOM:** React introduces the concept of the Virtual DOM, an in-memory representation of the real DOM. The Virtual DOM minimizes direct manipulation of the browser’s DOM, which is typically slow and can lead to complex, hard-to-maintain code. React updates the actual DOM only when necessary, ensuring that these updates are as efficient as possible. 

## Functional Components in React
### Learning Notes on Functional Components in React


#### 0. What is a Functional Component?
- **Definition**: A functional component in React is essentially a JavaScript function that takes in inputs and returns JSX (JavaScript XML) to define what the UI should look like. It’s similar to how a regular JavaScript function operates, where it takes some input, processes it, and returns an output.

#### 1. JSX (JavaScript XML)
- **Introduction to JSX**: JSX is a syntax extension for JavaScript that looks a lot like HTML but is used in React to describe what the UI should look like. Even though it looks like HTML, JSX can incorporate JavaScript logic directly within it.

- **Example**: When writing JSX inside a functional component, you can return HTML-like code. However, this code isn't exactly HTML—it's JSX, and it needs to be transpiled (converted) into actual HTML that the browser can understand (converted react framework).
  - **Example Code**:
    ```javascript
    function Heading() {
      const title = "This is some heading text";
      return (<h1>{title}</h1>);
    }
    ```
    - Here, `<h1>{title}</h1>` is JSX. The curly braces `{}` are used to insert JavaScript expressions within the JSX.

#### 3. Creating a Functional Component
- **Steps to Create a Functional Component**:
  1. **Naming**: Start by naming your component with a capital letter (e.g., `Heading`). React differentiates between HTML elements and React components based on whether the name is capitalized.
  2. **Function Declaration**: Define your functional component as a JavaScript function.
  3. **Returning JSX**: Inside the function, return JSX to describe the UI.
  4. **Using the Component**: Just like how you call a function in JavaScript, you can use the component by including it as a JSX tag in another component.

- **Example**:
  ```javascript
  function Heading() {
    const title = "This is some heading text";
    return (<h1>{title}</h1>);
  }

  // Usage in another component
  function App() {
    return (
      <div>
        <Heading />
      </div>
    );
  }
  ```


## Set up a react project
0. Install Node.js runtime

  ```bash
  # Verify npm installation
  npm -version
  ```



1. React project init
``` bash
npm init react-app firstapp
cd /firstapp
npm start react
#Note, "npm install react"  is incorrect.
# Adding HOST= can expose the server to local network access. To access the server via another device may require firewall configuration
HOST=0.0.0.0 npm start
```

## React Project Structure
0. /node_modules
- Contains all the modules required for the React app.
- Automatically populated when installing npm packages.

1. /public
- Houses assets displayed in the app (e.g., logos, favicon).
- important files
  - **index.html**: The main HTML file where the React app is injected.
  - **robots.txt**: Used for SEO purposes.
  - **manifest.json**: Provides metadata for the app when installed on a device.
 

2. /src
- Source code files for the React app.
- important files
  - **App.js**: The root component of the app.
  - **index.js**: The entry point that imports everything needed to render the app.
  - **App.test.js, setupTests.js, reportWebVitals.js**: Related to app performance and testing.
  - **App.css & index.css**: Stylesheets for the app components and overall application.

## React Components, Modules
---------

0. **Import and Export Statements**: 
  - **Export**: Makes a module available to other files.
  - **Import**: Allows a module to be brought into a file for use.

1. Types of Exports
- **Default Export**: Used when the function name is the same as the file name.
- **Named Export**: Used when the function name differs from the file name.

2. Differentiating Components and Modules
- **Components**: Typically represent a single piece of UI, like a button.
- **Modules**: Can be thought of as a collection of components or a larger functionality.



