# SQL_task2

DROP TABLE IF EXISTS ReturnedBooks;
DROP TABLE IF EXISTS IssuedBooks;
DROP TABLE IF EXISTS BookCategories;
DROP TABLE IF EXISTS Librarians;
DROP TABLE IF EXISTS Books;
DROP TABLE IF EXISTS Users;


CREATE TABLE IF NOT EXISTS Users (
    user_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE,
    phone VARCHAR(15)
);

CREATE TABLE IF NOT EXISTS Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(150),
    author VARCHAR(100),
    publisher VARCHAR(100),
    isbn VARCHAR(20) UNIQUE
);

CREATE TABLE IF NOT EXISTS Librarians (
    librarian_id INT PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
);

CREATE TABLE IF NOT EXISTS IssuedBooks (
    issue_id INT PRIMARY KEY,
    user_id INT,
    book_id INT,
    issue_date DATE,
    due_date DATE,
    FOREIGN KEY (user_id) REFERENCES Users(user_id),
    FOREIGN KEY (book_id) REFERENCES Books(book_id)
);

CREATE TABLE IF NOT EXISTS ReturnedBooks (
    return_id INT PRIMARY KEY,
    issue_id INT,
    return_date DATE,
    fine DECIMAL(6,2),
    FOREIGN KEY (issue_id) REFERENCES IssuedBooks(issue_id)
);

CREATE TABLE IF NOT EXISTS BookCategories (
    category_id INT PRIMARY KEY,
    category_name VARCHAR(50)
);


INSERT INTO Users (user_id, name, email, phone) VALUES 
(1, 'Anita Sharma', 'anita@gmail.com', '9876543210'),
(2, 'Ravi Kumar', 'ravi.k@gmail.com', NULL),
(3, 'Sonal Mehta', 'sonal.m@gmail.com', '9988776655');


INSERT INTO Books (book_id, title, author, publisher, isbn) VALUES 
(101, 'Data Structures in C', 'Narasimha Karumanchi', 'CareerMonk', '9788193245279'),
(102, 'Clean Code', 'Robert C. Martin', 'Prentice Hall', '9780132350884'),
(103, 'Introduction to Algorithms', 'CLRS', 'MIT Press', '9780262033848');

INSERT INTO Librarians (librarian_id, name, email) VALUES 
(1, 'Priya Desai', 'priya.d@library.com'),
(2, 'Amit Verma', 'amit.v@library.com');


INSERT INTO BookCategories (category_id, category_name) VALUES 
(1, 'Computer Science'),
(2, 'Programming'),
(3, 'Algorithms');

INSERT INTO IssuedBooks (issue_id, user_id, book_id, issue_date, due_date) VALUES 
(1001, 1, 101, '2025-06-01', '2025-06-15'),
(1002, 2, 102, '2025-06-05', '2025-06-20'),
(1003, 3, 103, '2025-06-10', '2025-06-25');

INSERT INTO ReturnedBooks (return_id, issue_id, return_date, fine) VALUES 
(201, 1001, '2025-06-14', 0.00),
(202, 1002, '2025-06-25', 10.00);

UPDATE Users
SET phone = '9112233445'
WHERE user_id = 2;

UPDATE Books
SET publisher = 'Pearson'
WHERE book_id = 102;

UPDATE ReturnedBooks
SET fine = 5.00
WHERE return_id = 202;


DELETE FROM ReturnedBooks
WHERE return_id = 201;

DELETE FROM IssuedBooks
WHERE issue_id = 1003;

DELETE FROM Users
WHERE user_id = 3;
