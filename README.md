# NPM Demo - Node.js HTTP Server

A simple Node.js HTTP server project demonstrating core concepts including request handling, file system operations, and form data processing.

## 📋 Project Overview

This is a basic Node.js application that creates an HTTP server capable of:
- Serving HTML forms
- Handling POST requests
- Writing user input to files
- Routing different URL paths

## 🚀 Features

- **Home Route (`/`)**: Displays an HTML form with a text input
- **Message Route (`/message`)**: Handles POST requests and saves form data to a file
- **Default Route**: Displays a simple "Hello" message for all other routes
- **File System Integration**: Writes user messages to `message.txt`
- **Modular Code Structure**: Separates routing logic into its own module

## 📁 Project Structure

```
npm-demo/
├── .vscode/
│   └── launch.json          # VSCode debugger configuration
├── node_modules/            # Dependencies (not tracked in git)
├── app.js                   # Main application entry point
├── routes.js                # Request handler and routing logic
├── index.js                 # Empty placeholder file
├── message.txt              # Generated file containing user messages
├── package.json             # Project metadata and dependencies
└── package-lock.json        # Locked dependency versions
```

## 🛠️ Technologies Used

- **Node.js**: Runtime environment
- **HTTP Module**: Built-in Node.js module for creating servers
- **File System (fs)**: Built-in module for file operations
- **Nodemon**: Development dependency for auto-reloading

## 📦 Dependencies

### Production Dependencies
- `express`: ^5.2.1 (installed but not currently used in the code)
- `underscore`: ^1.13.7 (installed but not currently used in the code)

### Development Dependencies
- `nodemon`: ^3.1.11 - Automatically restarts the server on file changes

## ⚙️ Installation

1. **Clone or download the project**

2. **Install dependencies**
   ```bash
   npm install
   ```

## 🎯 Usage

### Start the server (with auto-reload)
```bash
npm start
```
This runs `nodemon app.js` and will automatically restart on code changes.

### Start the server (without auto-reload)
```bash
npm run start-server
```
This runs `node app.js` for production use.

### Access the application
Open your browser and navigate to:
```
http://localhost:3000
```

## 🔄 How It Works

### 1. **Server Creation** (`app.js`)
```javascript
const server = http.createServer(routes.handler)
server.listen(3000)
```
- Creates an HTTP server using the request handler from `routes.js`
- Listens on port 3000

### 2. **Request Routing** (`routes.js`)

#### **Home Route (`/`)**
- Displays an HTML form with:
  - Text input field
  - Submit button
  - Form action pointing to `/message`

#### **Message Route (`/message` + POST)**
- Receives form data via POST request
- Listens for data chunks using streams
- Parses the form data (`message=userInput`)
- Writes the message to `message.txt`
- Redirects user back to home (`/`)

#### **Default Route**
- Returns a simple HTML page with "Hello" message
- Serves for any unmatched routes

### 3. **Module Exports**
```javascript
module.exports = {
    handler: requestHandler,
    someText: "Some coded Text"
}
```
- Exports the request handler function
- Demonstrates multiple export properties

## 📝 Code Walkthrough

### Form Data Processing
```javascript
const body = []
req.on('data', (chunk) => {
    body.push(chunk)
})
req.on('end', () => {
    const parsedBody = Buffer.concat(body).toString()
    const message = parsedBody.split("=")[1]
    fs.writeFileSync('message.txt', message)
})
```

**How it works:**
1. Collects incoming data chunks into an array
2. Concatenates chunks into a Buffer
3. Converts Buffer to string
4. Parses form data format (`message=value`)
5. Writes extracted message to file

### Response Headers
```javascript
res.statusCode = 302              // Redirect status
res.setHeader('Location', '/')    // Redirect destination
res.setHeader('Content-Type', 'text/html')
```

## 🖥️ Screenshots

### Development Environment
The project runs in VS Code with:
- Terminal showing `npm run start` output
- Server running on `localhost:3000`
- File explorer showing project structure

### Browser Interface
- Simple form interface at `http://localhost:3000`
- Text input field for entering messages
- Send button to submit form

## 🐛 Known Issues / Limitations

1. **Synchronous File Writing**: Uses `fs.writeFileSync()` which blocks the event loop
   - **Better approach**: Use `fs.writeFile()` for async operations

2. **No Error Handling**: No try-catch blocks or error handlers

3. **URL Encoding**: Doesn't handle URL-encoded special characters properly

4. **Security**: No input validation or sanitization

5. **Unused Dependencies**: Express and Underscore are installed but not used

## 🔧 Potential Improvements

- [ ] Replace `fs.writeFileSync()` with async `fs.writeFile()`
- [ ] Add proper error handling
- [ ] Implement URL decoding for form data
- [ ] Add input validation and sanitization
- [ ] Remove unused dependencies
- [ ] Add environment variables for configuration
- [ ] Implement proper logging
- [ ] Add unit tests

## 📚 Learning Concepts

This project demonstrates:
- ✅ Creating HTTP servers in Node.js
- ✅ Handling different HTTP methods (GET, POST)
- ✅ URL routing
- ✅ Form data parsing
- ✅ File system operations
- ✅ Response redirects
- ✅ Module exports and imports
- ✅ Stream-based data handling


## 🤝 Contributing

This is a learning/demo project. Feel free to fork and experiment!

---

**Note**: This is a basic educational project demonstrating core Node.js concepts. For production applications, consider using frameworks like Express.js for better structure, security, and features.
