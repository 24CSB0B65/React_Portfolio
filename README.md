Project Overview

This project is a personal portfolio website developed using React and Vite. It contains separate pages for the Home, About, Projects, Project Details, Contact, and Not Found sections. The project demonstrates reusable React components, React Router navigation, props, state management, state lifting, controlled forms, form validation, and React useEffect hooks.

Setup and Run Instructions

Make sure Node.js and npm are installed on the computer.

Open a terminal and navigate to the project folder.

Install the required dependencies by running:

npm install

Start the development server by running:

npm run dev

Open the local URL displayed in the terminal in a web browser. With Vite, this is normally:

http://localhost:5173/

To create a production build, run:

npm run build

To preview the production build locally, run:

npm run preview

Component Tree

The application starts from main.jsx, which loads App.jsx. App.jsx contains the routing and the common application layout. The Navbar and Footer are reusable components. The pages are displayed according to the current URL.

The main component structure is:

App

 ├── Navbar

 ├── Home

 ├── About

 ├── Projects

 │    └── ProjectCard

 │         └── ProjectInfo

 ├── ProjectDetails

 ├── Contact

 │    └── ContactForm

 ├── NotFound

 └── Footer

The project information is stored separately in the projects data file. The Projects page passes project information to reusable ProjectCard components through props. ProjectCard can then pass required information to ProjectInfo. This avoids repeating the same project markup for every project.

State-Lifting Decisions

The dark/light theme state is maintained in the top-level App component because the theme is an application-level setting that can affect multiple parts of the website. App stores the current theme and contains the function that changes between light and dark mode.

The theme and the theme-changing function are passed from App to the layout and then to Navbar through props. The Navbar uses these props to display and change the theme. This is state lifting because the shared state is maintained by a common parent rather than separately inside Navbar.

The selected theme is also stored in localStorage so that the user's theme preference remains after refreshing the page.

Controlled Contact Form and Validation

The contact form is implemented as a controlled React form in ContactForm.jsx. The name, email, and message fields are stored in React state. Each input receives its value from state and uses an onChange handler to update the state whenever the user types.

The form also maintains an errors object in state. The validation function checks that the name and message are not empty and that the email field is filled and follows a basic valid email format. Validation messages are displayed beside the relevant fields.

The submit button is disabled while required fields are empty or invalid. Once all required fields are valid, the button becomes enabled. After a valid submission, a success message is displayed and the form is cleared.

React Router Navigation

React Router is used to navigate between the different pages without completely reloading the browser. The Navbar uses NavLink components for navigation links such as Home, About, Projects, and Contact. The corresponding routes are defined in App.jsx.

The project also contains a dynamic project-details route so that an individual project can be displayed based on its project ID. A NotFound route handles URLs that do not match an existing page.

useEffect Hooks Used in the Project

1. App.jsx – Theme Persistence

The useEffect hook in App.jsx runs whenever the selected theme changes. It stores the current theme in localStorage and updates the data-theme attribute on the document's root HTML element. The CSS uses this attribute to apply the light or dark theme. This effect is necessary because localStorage and the document element are external to React's normal rendering process.

2. Navbar.jsx – Window Resize Handling

The Navbar uses useEffect to listen for browser window resize events. It checks the window width to determine whether the navigation should behave as a mobile or desktop navigation. The effect removes the resize listener when the component is unmounted. This cleanup is necessary to avoid leaving an unnecessary event listener active.

3. Home.jsx – Loading State

The Home page uses useEffect to manage its initial loading behavior. A short timer is started when the page loads, and after the timer finishes the loading state is changed so the main Home page content can be displayed. The timer is cleared when the component is unmounted so that it does not continue unnecessarily.

Summary

The project is organized into reusable components and separate pages so that each part of the website has a clear responsibility. Shared application state such as the theme is maintained in App.jsx and passed to components through props. Local state such as contact form values and validation errors is maintained inside the component that uses it.

React Router handles page navigation. The useEffect hooks are used for side effects such as theme persistence, window resize handling, and the Home page loading timer. Together, these features demonstrate the main React concepts required for the portfolio project.
