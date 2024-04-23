# Library-management-system
/////////////////


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Library Management System</title>
    <style>
        /* Global Styles */
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }

        .back-button {
            margin-bottom: 20px;
        }

        /* Login Form Styles */
        .login-container {
            width: 300px;
            margin: 50px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        .login-container h2 {
            text-align: center;
            margin-bottom: 20px;
        }

        .login-container input[type="text"],
        .login-container input[type="password"] {
            width: calc(100% - 20px);
            margin-bottom: 15px;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 4px;
        }

        .login-container input[type="submit"] {
            width: 100%;
            padding: 10px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        .login-container input[type="submit"]:hover {
            background-color: #0056b3;
        }

        /* Book Management Styles */
        .book-management-container {
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            padding: 20px;
        }

        .book-management-container h2 {
            text-align: center;
            margin-bottom: 20px;
        }

        .book-table {
            width: 100%;
            border-collapse: collapse;
        }

        .book-table th,
        .book-table td {
            padding: 10px;
            border-bottom: 1px solid #ddd;
        }

        .book-table th {
            background-color: #f2f2f2;
            text-align: left;
        }

        .book-table tr:hover {
            background-color: #f9f9f9;
        }

        .button {
            padding: 8px 16px;
            background-color: #007bff;
            color: #fff;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }

        .button:hover {
            background-color: #0056b3;
        }
    </style>
</head>
<body>
    <!-- Login Form -->
    <div class="container">
        <div class="login-container">
            <h2>Library Management System</h2>
            <form id="loginForm">
                <input type="text" name="username" placeholder="Username" required><br>
                <input type="password" name="password" placeholder="Password" required><br>
                <input type="submit" value="Login">
            </form>
        </div>
    </div>

    <!-- Book Management -->
    <div class="container book-management-container" style="display: none;">
        <button class="back-button" onclick="goBack()">Back</button>
        <h2>Library Catalog</h2>
        <table class="book-table">
            <thead>
                <tr>
                    <th>Title</th>
                    <th>Author</th>
                    <th>Publication Year</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody id="bookList">
                <!-- Book rows will be dynamically added here -->
            </tbody>
        </table>
        <button class="button" id="addBookButton">Add Book</button>
    </div>

    <!-- Modal for adding/editing book details -->
    <div id="myModal" class="modal" style="display: none;">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <h2>Add/Edit Book</h2>
            <form id="bookForm">
                <input type="text" name="title" placeholder="Title" required><br>
                <input type="text" name="author" placeholder="Author" required><br>
                <input type="number" name="publicationYear" placeholder="Publication Year" required><br>
                <input type="submit" value="Save">
            </form>
        </div>
    </div>

    <script>
        // JavaScript for handling user login
        const loginForm = document.getElementById('loginForm');
        const bookManagementContainer = document.querySelector('.book-management-container');
        const bookList = document.getElementById('bookList');

        loginForm.addEventListener('submit', function (event) {
            event.preventDefault();
            // Simulate login (for demonstration purposes)
            const username = this.username.value;
            const password = this.password.value;
            if (username === 'admin' && password === 'password') {
                // Display book management section
                bookManagementContainer.style.display = 'block';
                // Hide login section
                this.parentElement.style.display = 'none';
                // Load books data (for demonstration purposes)
                loadBooks();
            } else {
                alert('Invalid username or password. Please try again.');
            }
        });

        // JavaScript for handling book management
        const addBookButton = document.getElementById('addBookButton');
        const bookForm = document.getElementById('bookForm');
        const modal = document.getElementById('myModal');

        addBookButton.addEventListener('click', function () {
            modal.style.display = 'block';
        });

        function closeModal() {
            modal.style.display = 'none';
        }

        bookForm.addEventListener('submit', function (event) {
            event.preventDefault();
            // Save book data (for demonstration purposes)
            const title = this.title.value;
            const author = this.author.value;
            const publicationYear = this.publicationYear.value;
            // Add book to the list (for demonstration purposes)
            const bookRow = `
            <tr>
                <td>${title}</td>
                <td>${author}</td>
                <td>${publicationYear}</td>
                <td><button class="button">Remove</button></td>
            </tr>`;
            bookList.insertAdjacentHTML('beforeend', bookRow);
            // Clear form fields
            this.reset();
            // Close modal
            closeModal();
        });

        // JavaScript for handling book removal
        bookList.addEventListener('click', function (event) {
            if (event.target.classList.contains('button')) {
                event.target.parentElement.parentElement.remove();
            }
        });

        // Function to load books data (for demonstration purposes)
        function loadBooks() {
            // Simulated books data (for demonstration purposes)
            const books = [
                { title: 'To Kill a Mockingbird', author: 'Harper Lee', publicationYear: 1960 },
                { title: '1984', author: 'George Orwell', publicationYear: 1949 },
                { title: 'Pride and Prejudice', author: 'Jane Austen', publicationYear: 1813 },
                // Add more book data here...
            ];
            // Display books in the list (for demonstration purposes)
            books.forEach(book => {
                const bookRow = `
                <tr>
                    <td>${book.title}</td>
                    <td>${book.author}</td>
                    <td>${book.publicationYear}</td>
                    <td><button class="button">Remove</button></td>
                </tr>`;
                bookList.insertAdjacentHTML('beforeend', bookRow);
            });
        }

        // JavaScript function to go back to the previous page
        function goBack() {
            window.history.back();
        }
    </script>
</body>
</html>
