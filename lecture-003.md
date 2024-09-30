# Lecture #003 📌

# **\<u>Lecture 3: Building a Simple API Server Using JavaScript Objects and Arrays\</u>**

In this lecture, we will create a simple API server using **Node.js** and **Express**. We will manage user data using JavaScript objects and arrays, demonstrating basic CRUD operations (Create, Read, Update, Delete).

***

### **Topics Covered in Lecture 3:**

1\. **What is an API?**

2\. **Setting Up the Development Environment**

3\. **Creating an Express Server**

4\. **Using JavaScript Objects and Arrays for Data Storage**

5\. **Performing CRUD Operations**

6\. **Testing the API**

7\. **Summary**

***

![](assets/nukubILx0KDMIvVFrk-OX96S3tAiDR5H_OD_cMkDoKE=.png)

**\<u>LIVE CODE\</u>**

```javascript

const express = require('express');

const jwt = require('jsonwebtoken');

const app = express();

app.use(express.json());

app.listen(9000,

    () => {

        console.log("Server is running on port number 9000 .....")

    }

)

app.get('/users', (req, res) => {

    const token = req.headers.authorization;

    if (!token) {

        return res.status(401).json({ message: "Unauthorized, no token provided." });

    }

    jwt.verify(token, "SECRET_KEY", (err, user) => {

        if (err) {

            return res.status(401).json({ message: "Unauthorized, invalid token." });

        }

        const users = { name: "Muhammad Qazi", email: "test@test.com" };

        res.status(200).json(users);

    });

});

app.post('/login', (req, res) => {

    const usersData = req.body;

    if (usersData.email === "test@gmail.com" && usersData.password === "1234qwer") {

        const payload = {

            email: usersData.email

        };

        const token = jwt.sign(payload, "SECRET_KEY", { expiresIn: "1h" })

        res.status(200).json({ message: "Sucessfully authenticated", token: token });

    } else {

        res.status(401).json({ message: "Not allowed" })

    }

})

app.patch('/users/:id', (req, res) => {

    const pathParams = req.params;

    const users = { id: 1, name: "Muhamad", password: "password" }

    res.status(200).json(users);

})

```

### 1. **What is an API?**

An **API (Application Programming Interface)** allows different software applications to communicate with each other. In web development, APIs allow clients (like web browsers or mobile apps) to request and exchange data with a server.

For example, a weather app may use an API to fetch the current weather data from a server.

***

### 2. **Setting Up the Development Environment**

#### **Install Node.js**

Make sure you have Node.js installed. You can download it from the [official Node.js website](https://nodejs.org/).

#### **Create a New Project**

1\. Create a new project directory:

   ```shellscript

   mkdir simple-api-server

   cd simple-api-server

   ```

&#x20;  \`\`\`

1\. Initialize the project:

   ```shellscript

   npm init -y

   ```

&#x20;  \`\`\`

1\. Install Express:

   ```shellscript

   npm install express

   ```

&#x20;  \`\`\`

***

### 3. **Creating an Express Server**

Now, let's create a basic Express server to handle API requests.

#### **Step 1: Create ****`index.js`**

Create a file called `index.js` in your project directory and set up the Express server:

```javascript

const express = require('express');

const app = express();

const PORT = 3000;

// Middleware to parse JSON request bodies

app.use(express.json());

// Sample data: an array to store users

let users = [];

// Start the server

app.listen(PORT, () => {

    console.log(`Server running on http://localhost:${PORT}`);

});

```

#### **Step 2: Run the Server**

```shellscript

node index.js

```

You should see a message in your terminal: `Server running on http://localhost:3000`. Open your browser or Postman and visit `http://localhost:3000` to see that the server is running.

***

### 4. **Using JavaScript Objects and Arrays for Data Storage**

We will use an array called `users` to store user objects. Each user will be represented as an object with properties like `id`, `name`, and `email`.

#### **Example User Object**

```javascript

let users = [

    { id: 1, name: 'John Doe', email: 'john@example.com' },

    { id: 2, name: 'Jane Smith', email: 'jane@example.com' }

];

```

***

### 5. **Performing CRUD Operations**

#### **GET: Retrieve All Users**

Add a route to fetch all users:

```javascript

app.get('/users', (req, res) => {

    res.json(users); // Respond with the users array

});

```

#### **POST: Add a New User**

Add a route to create a new user:

```javascript

app.post('/users', (req, res) => {

    const newUser = req.body; // Get user data from the request body

    users.push(newUser); // Add the new user to the users array

    res.status(201).json(newUser); // Respond with the newly created user

});

```

#### **PUT: Update an Existing User**

Add a route to update an existing user:

```javascript

app.put('/users/:id', (req, res) => {

    const { id } = req.params; // Get user ID from the URL

    const updatedUser = req.body; // Get updated user data from the request body

    // Find the user by ID and update it

    const userIndex = users.findIndex(user => user.id == id);

    if (userIndex !== -1) {

        users[userIndex] = { ...users[userIndex], ...updatedUser }; // Update the user

        res.json(users[userIndex]); // Respond with the updated user

    } else {

        res.status(404).json({ message: 'User not found' }); // User not found

    }

});

```

#### **DELETE: Remove a User**

Add a route to delete a user:

```javascript

app.delete('/users/:id', (req, res) => {

    const { id } = req.params; // Get user ID from the URL

    // Find the user by ID and remove it

    users = users.filter(user => user.id != id); // Remove the user

    res.status(204).send(); // Respond with no content

});

```

***

### 6. **Testing the API**

You can test the API using **Postman** or **curl**. Here are some examples of how to interact with the API.

#### **GET: Fetch All Users**

```shellscript

curl -X GET http://localhost:3000/users

```

#### **POST: Create a New User**

```shellscript

curl -X POST http://localhost:3000/users -H "Content-Type: application/json" -d '{"id": 3, "name": "Alice Johnson", "email": "alice@example.com"}'

```

#### **PUT: Update an Existing User**

```shellscript

curl -X PUT http://localhost:3000/users/1 -H "Content-Type: application/json" -d '{"name": "John Doe Updated", "email": "john.updated@example.com"}'

```

#### **DELETE: Remove a User**

curl -X DELETE http://localhost:3000/users/2

Let's enhance the previous lecture to include **JWT (JSON Web Tokens)** for authorization. This will help beginners understand how to implement authentication in a simple API server. We'll focus on using JWT middleware to protect routes and manage user sessions.

### **Lecture 3.1: Building an API Server with JWT Authorization**

In this lecture, we will extend our previous API server to include JWT-based authentication. We'll cover how to create a JWT, use it to authorize users, and implement middleware to protect our API routes.

***

### **Topics Covered in Lecture 4:**

1\. **What is JWT?**

2\. **Setting Up JWT in Our API**

3\. **Creating JWTs for Authentication**

4\. **Protecting Routes with JWT Middleware**

5\. **Testing the API with JWT**

6\. **Summary**

***

### 1. **What is JWT?**

**JWT (JSON Web Token)** is a compact and self-contained way to represent information between two parties. It is commonly used for authentication and information exchange. A JWT is typically composed of three parts:

* **Header**: Contains the type of the token (JWT) and the signing algorithm (e.g., HMAC SHA256).

* **Payload**: Contains the claims (the information you want to transmit), such as user ID and roles.

* **Signature**: Used to verify that the sender of the JWT is who it says it is and to ensure that the message wasn't changed along the way.

### Example JWT Structure:

```

eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

```

***

### 2. **Setting Up JWT in Our API**

#### **Install JWT Library**

To handle JWTs, we'll use the `jsonwebtoken` library. First, install it in your project:

```shellscript

npm install jsonwebtoken

```

#### **Import JWT in ****`index.js`**

At the top of your `index.js` file, import the required modules:

```javascript

const express = require('express');

const jwt = require('jsonwebtoken');

const app = express();

const PORT = 3000;

// Middleware to parse JSON request bodies

app.use(express.json());

// Sample data: an array to store users

let users = [];

const SECRET_KEY = 'your_secret_key'; // Replace with a strong secret

```

***

### 3. **Creating JWTs for Authentication**

We will create a route to authenticate users and generate a JWT.

#### **Authentication Route**

Add a route for user authentication:

```javascript

app.post('/login', (req, res) => {

    const { name, email } = req.body;

    // In a real application, you would verify the user's credentials

    const user = { name, email }; // Mock user object

    const token = jwt.sign(user, SECRET_KEY, { expiresIn: '1h' }); // Create a JWT

    res.json({ token }); // Respond with the token

});

```

***

### 4. **Protecting Routes with JWT Middleware**

To protect certain routes, we need to create middleware that verifies the JWT:

#### **JWT Middleware**

Create a middleware function to verify the token:

```javascript

function authenticateToken(req, res, next) {

    const token = req.headers['authorization']?.split(' ')[1]; // Get token from Authorization header

    if (!token) return res.sendStatus(401); // No token provided

    jwt.verify(token, SECRET_KEY, (err, user) => {

        if (err) return res.sendStatus(403); // Invalid token

        req.user = user; // Attach user info to request

        next(); // Proceed to the next middleware/route handler

    });

}

```

#### **Protect Routes Using Middleware**

Now, we can protect our existing routes (e.g., getting users) with this middleware:

```javascript

app.get('/users', authenticateToken, (req, res) => {

    res.json(users); // Respond with the users array

});

```

***

### 5. **Testing the API with JWT**

#### **Test the Login Route**

Use Postman or curl to test the login route:

```shellscript

curl -X POST http://localhost:3000/login -H "Content-Type: application/json" -d '{"name": "John Doe", "email": "john@example.com"}'

```

You should receive a response containing a JWT:

```json

{

    "token": "your_jwt_token_here"

}

```

#### **Use the Token to Access Protected Routes**

Now, use the received JWT to access protected routes. Include it in the `Authorization` header:

```shellscript

curl -X GET http://localhost:3000/users -H "Authorization: Bearer your_jwt_token_here"

```

If the token is valid, you should receive a list of users.

***

### Certainly! Below is a simple example of a login API implemented using Node.js and Express without a database. Instead of a database, we'll use an in-memory object to simulate user data for authentication purposes. This is suitable for demonstration or testing purposes.

### **Login API Example Without a Database**

#### **1. Setup the Project**

1\. **Initialize a New Node.js Project**

   ```shellscript

   mkdir login-api

   cd login-api

   npm init -y

   ```

&#x20;  \`\`\`

1\. **Install Required Packages**

   ```shellscript

   npm install express jsonwebtoken

   ```

&#x20;  \`\`\`

#### **2. Create the API**

1\. **Create an ****`index.js`**** File**

&#x20;  Create a file named `index.js` in your project directory.

````javascript

const express = require('express');

const jwt = require('jsonwebtoken');

const app = express();

const PORT = 3000;

// Middleware to parse JSON request bodies

app.use(express.json());

// In-memory user data (simulating a database)

const users = [

    { username: 'user1', password: 'password1' },

    { username: 'user2', password: 'password2' },

];

const SECRET_KEY = 'your_secret_key'; // Replace with a strong secret

// Login route

app.post('/login', (req, res) => {

    const { username, password } = req.body;

    // Find user in the in-memory users array

    const user = users.find(u => u.username === username && u.password === password);

    if (user) {

        // Generate JWT token

        const token = jwt.sign({ username: user.username }, SECRET_KEY, { expiresIn: '1h' });

        return res.json({ token }); // Respond with the token

    } else {

        return res.status(401).json({ message: 'Invalid credentials' }); // Unauthorized

    }

});

// Protected route example

app.get('/protected', (req, res) => {

    const authHeader = req.headers['authorization'];

    const token = authHeader && authHeader.split(' ')[1]; // Get token from Authorization header

    if (!token) return res.sendStatus(401); // No token provided

    // Verify token

    jwt.verify(token, SECRET_KEY, (err, user) => {

        if (err) return res.sendStatus(403); // Invalid token

        res.json({ message: 'This is a protected route', user }); // Access granted

    });

});

// Start the server

app.listen(PORT, () => {

    console.log(`Server is running on http://localhost:${PORT}`);

});

&#x20;  ```

#### **3. Run the API**

In the terminal, run:

```bash

node index.js

````

You should see the message indicating that the server is running.

#### **4. Testing the API**

You can use tools like **Postman** or **cURL** to test the API.

1\. **Login Request**

   * **URL**: `http://localhost:3000/login`

   * **Method**: `POST`

   * **Body** (JSON):

     ```json

     {

         "username": "user1",

         "password": "password1"

     }

     ```

### **Git Basics**

***

### **Topics Covered:**

1\. **What is Git?**

2\. **Setting Up Git**

3\. **Basic Git Commands**

4\. **Creating a New Repository**

5\. **Working with Remote Repositories**

6\. **Pushing Changes**

7\. **Cloning a Repository**

8\. **Branching and Merging**

9\. **Basic Git Workflow**

10\. **Conclusion**

***

### **1. What is Git?**

* **Git** is a distributed version control system that helps developers manage and track changes to code and other files in a project.

* It allows multiple developers to work on a project simultaneously without overwriting each other's changes.

* Git keeps a history of changes, making it easy to revert to previous versions if needed.

### **2. Setting Up Git**

To start using Git, you need to install it on your machine. Here's how to do it:

#### **Installation**

* **Windows**: Download Git from [git-scm.com](https://git-scm.com/download/win) and follow the installer instructions.

* **macOS**: You can install Git using Homebrew:

  ```shellscript

  brew install git

  ```

&#x20; \`\`\`

* **Linux**: Use your package manager, for example:

  ```shellscript

  sudo apt-get install git  # For Debian/Ubuntu

  ```

&#x20; \`\`\`

#### **Configuration**

After installation, configure your Git username and email (this is important for commit history):

```shellscript

git config --global user.name "Your Name"

git config --global user.email "you@example.com"

```

### **3. Basic Git Commands**

* **Check Git Version**:

  ```shellscript

  git --version

  ```

&#x20; \`\`\`

* **Initialize a New Repository**:

  ```shellscript

  git init

  ```

&#x20; \`\`\`

* **Clone a Repository**:

  ```shellscript

  git clone <repository-url>

  ```

&#x20; \`\`\`

* **Check Status of Files**:

  ```shellscript

  git status

  ```

&#x20; \`\`\`

* **Add Files to Staging Area**:

  ```shellscript

  git add <file-name>  # For a specific file

  git add .            # To add all changes

  ```

&#x20; \`\`\`

* **Commit Changes**:

  ```shellscript

  git commit -m "Your commit message"

  ```

&#x20; \`\`\`

* **View Commit History**:

  ```shellscript

  git log

  ```

&#x20; \`\`\`

### **4. Creating a New Repository**

1\. **Create a New Directory**:

   ```shellscript

   mkdir my-project

   cd my-project

   ```

&#x20;  \`\`\`

1\. **Initialize Git**:

   ```shellscript

   git init

   ```

&#x20;  \`\`\`

1\. **Create a File**:

   ```shellscript

   echo "Hello, Git!" > README.md

   ```

&#x20;  \`\`\`

1\. **Check Status**:

   ```shellscript

   git status

   ```

&#x20;  \`\`\`

1\. **Add the File**:

   ```shellscript

   git add README.md

   ```

&#x20;  \`\`\`

1\. **Commit the File**:

   ```shellscript

   git commit -m "Initial commit"

   ```

&#x20;  \`\`\`

### **5. Working with Remote Repositories**

To collaborate with others, you'll often need to work with remote repositories (e.g., on GitHub).

1\. **Add a Remote Repository**:

   ```shellscript

   git remote add origin <repository-url>

   ```

&#x20;  \`\`\`

1\. **Push Changes to Remote**:

   ```shellscript

   git push -u origin master  # Push to the master branch

   ```

&#x20;  \`\`\`

### **6. Pushing Changes**

Once you've made changes and committed them, you can push your changes to the remote repository.

1\. **Make Changes** (edit files in your project).

2\. **Check Status**:

   ```shellscript

   git status

   ```

&#x20;  \`\`\`

3\. **Add Changes**:

```shellscript

   git add .

```

1\. Commit Changes

```shellscript

git commit -m "Describe your changes here"

```

1\. Push to remote

```shellscript

   git push origin master

```

### **7. Cloning new repository from github**

```

git clone <repository-url>

```

### **8. Branching and Merging**

* **Create a New Branch**:

  ```shellscript

  git branch <branch-name>

  ```

&#x20; \`\`\`

* **Switch to the Branch**:

  ```shellscript

  git checkout <branch-name>

  ```

&#x20; \`\`\`

* **Merge Branch**:

  &#x20; Switch to the branch you want to merge into (e.g., `master` or `main`) and then:

  ```shellscript

  git merge <branch-name>

  ```

&#x20; \`\`\`

### **9. Basic Git Workflow**

1\. **Make Changes**: Modify files in your project.

2\. **Check Status**: Use `git status` to see what has changed.

3\. **Add Changes**: Use `git add` to stage changes.

4\. **Commit Changes**: Use `git commit` to save changes locally.

5\. **Push Changes**: Use `git push` to send changes to the remote repository.

### **10. Conclusion**

* Git is an essential tool for developers, enabling version control and collaboration on code.

* Understanding the basics of Git allows you to manage projects effectively, track changes, and collaborate with other developers.

* As you become more familiar with Git, you can explore advanced features like rebasing, stash, and more.

***

### **Practical Example of Pushing Code**

1\. **Create a New Directory and Initialize Git**:

   ```shellscript

   mkdir my-example-project

   cd my-example-project

   git init

   ```

&#x20;  \`\`\`

1\. **Create a New File**:

   ```shellscript

   echo "This is my example project!" > example.txt

   ```

&#x20;  \`\`\`

1\. **Add and Commit**:

   ```shellscript

   git add example.txt

   git commit -m "Added example.txt"

   ```

&#x20;  \`\`\`

1\. **Create a Remote Repository** (on GitHub, GitLab, etc.), then run:

   ```shellscript

   git remote add origin <repository-url>

   git push -u origin master

   ```

&#x20;  \`\`\`

Now, your project should be pushed to the remote repository, and you can share it with others!

***