# Siemens | Vue.js Application (Airports CRUD)

A simple Vue.js application to manage a list of airports with CRUD (Create, Read, Update, Delete) operations.

## Requirements

To run this application locally, you need:

- Node.js - https://nodejs.org/ 
- npm - https://www.npmjs.com/

## Setup Instructions

1. **Clone the Repository**

   Open a terminal and clone the repository to your local machine:
   ```bash
   git clone <repository-url>
   cd <repository-folder>

2. **Install Dependencies**
   ```bash
   npm install

3. **Run the Application**
   ```bash
   npm run serve

4. **Access the Application**
   ```bash
   http://localhost:8080

## Technical Decisions

I chose a parent-child component structure, similar to what I learned in React. The **App.vue** component serves as the main container and manages the state of the application, while the **AirportForm** and **AirportList** components handle specific responsibilities:

- **App Component**: Manages the overall state and persists data in local storage. It interacts with child components through props and event emitters:
     - **Event emitters** allow the App component to listen for actions (such as adding, updating, or deleting an airport) from the child components.
     - **Props** pass data (list of airports) to the **AirportList Component**, enabling it to function correctly.
- **AirportForm Component**: Handles user input for adding new airports and emits an **add-airport** event to the parent.
- **AirportList Component**: Displays the list of airports and provides functionality for editing and deleting airports. It emits **delete-airport** and **update-airport** events to the parent.


      

