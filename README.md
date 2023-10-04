# Files-Patterns-and-Flags-in-JavaScript

## Table of Contents

- [File Objects ](#File-Objects )
- [FormData](#FormData)
- [Fetch: Cross-Origin Requests ](#Fetch:-Cross-Origin-Requests )
- [Patterns and Flags](#Patterns-and-Flags)


## File-Object
File and FileReader 

File and FileReader are classes commonly used in programming for reading files in various programming languages. They are part of the standard libraries in many languages, and they provide a way to interact with files on a computer's file system. 

File: 

In most programming languages, the File class represents a file on the file system. It provides methods and properties to perform operations like reading from, writing to, and managing files. 

 

File Reader 

The FileReader is like a special tool in a computer program that helps us read files. It's kind of like having a magical pair of glasses that lets you look inside a book and see what's written in it. 

 

Opening a Book: 

Imagine you have a book in your hand, but it's closed. You want to read what's inside. The FileReader is like a pair of magic glasses you put on to see inside the book. 

javascriptCopy code 

const reader = new FileReader(); 
 

Reading the Pages: 

Now that you have your magic glasses (FileReader), you can start reading the pages of the book. You can read them one page at a time or all at once. 

javascriptCopy code 

const file = new File(["Once upon a time..."], "storybook.txt", { type: "text/plain" }); 
 
reader.onload = (event) => { 
  console.log(event.target.result); 
}; 
 
reader.readAsText(file); 
 

In this example, you have a story ("Once upon a time...") in a special book. When you use the FileReader, it helps you see the story on your computer screen! 

 

Putting Away the Glasses: 

When you're done reading and you want to do something else, it's important to take off the magic glasses (close the FileReader). This helps save the magic energy. 

There isn't a specific command to "close" the FileReader, but it's like remembering to put away your toys when you're done playing with them! 

 

The main method is as follows: 

readAsArrayBuffer(blob) – read the data in binary format ArrayBuffer. 

readAsText(blob, [encoding]) – read the data as a text string with the given encoding (utf-8by default). 

readAsDataURL(blob) – read the binary data and encode it as base64 data url. 

abort() – cancel the operation. 

 

FileReader for blobs 

As mentioned in the chapter Blob, FileReadercan read not just files, but any blobs. 

We can use it to convert a blob to another format: 

readAsArrayBuffer(blob) – to ArrayBuffer, 

readAsText(blob, [encoding]) – to string (an alternative to TextDecoder), 

readAsDataURL(blob) – to base64 data url. 

FileReaderSync is available inside Web Workers 

For Web Workers, there also exists a synchronous variant of FileReader, called FileReaderSync. 

Its reading methods read* do not generate events, but rather return a result, as regular functions do. 

 

Fetch() 

The fetch() function in JavaScript is a modern way to make network requests, typically to retrieve data from a server or send data to a server. It is built into most modern web browsers and is used to work with APIs (Application Programming Interfaces) or fetch resources from URLs. 

Keep in mind that fetch() works in web browsers and in environments where there's a network connection available. If you're using JavaScript in a server-side environment (like Node.js), you'd use a different module or library to make network requests. 

 

 

Post Requests 

To make a POST request in JavaScript, you can use the fetch() function or other libraries like Axios or jQuery's AJAX. 

method – HTTP-method, e.g. POST, 

body – one of: 

a string (e.g. JSON), 

FormData object, to submit the data as form/multipart, 

Blob/BufferSource to send binary data, 

URLSearchParams, to submit the data in x-www-form-urlencoded encoding, rarely used. 

 

A POST request in web development is used to send data to a server to create or update a resource. This data can be in various formats, such as JSON, XML, or form data. Here are some common use cases for POST requests: 

Submitting Forms: When you fill out a form on a website and click "Submit", the data you entered is sent to the server using a POST request. This is how information like login details, registration information, and search queries get sent to the server. 

Creating Resources: When you want to add new information to a database, you use a POST request. For example, if you're using an app and you create a new post, comment, or user account, that information is sent to the server using a POST request. 

Uploading Files: If you're uploading a file (like an image or a document) to a website, it's typically done using a POST request. The file data is included in the request body. 

Sending Data Securely: POST requests are more secure than GET requests for sending sensitive information. With a POST request, the data is sent in the request body, which is not visible in the URL. 

API Endpoints: When you're working with APIs (Application Programming Interfaces), you often use POST requests to interact with the server. For example, if you're building a social media app, you might use a POST request to create a new post. 

Updating Resources: While GET requests are used for retrieving data, POST requests can also be used to update existing resources on the server. For example, if you're editing your profile information on a website, the updated data is sent with a POST request. 

Sending Data to Payment Gateways: When you make an online purchase, the data about your purchase (like the item, price, and payment details) is sent to the payment gateway using a POST request. 

Submitting Comments or Reviews: On websites with user-generated content, like forums or product review sites, when you submit a comment or review, that data is sent to the server via a POST request. 

 

 

Sending an Image 

To send an image using a POST request in JavaScript, you'll need to use the FormData object along with the fetch() function. 

Please note that handling file uploads involves considerations for security and file size limitations. You should validate and sanitize user input, set appropriate server-side file size limits, and handle file storage securely. 

## FormData
 

FormData is a JavaScript object that allows you to easily construct a set of key/value pairs representing form fields and their values. It's particularly useful when you want to send data via an HTTP request, such as using the fetch API or in an XMLHttpRequest. 

The constructor is: 

let formData = new FormData([form]); 

FormData is an object to store and send form data. 


Sending a simple form 


FormData Methods 

formData.append(name, value) – add a form field with the given name and value, 

formData.append(name, blob, fileName) – add a field as if it were <input type="file">, the third argument fileName sets file name (not form field name), as it it were a name of the file in user’s filesystem, 

formData.delete(name) – remove the field with the given name, 

formData.get(name) – get the value of the field with the given name, 

formData.has(name) – if there exists a field with the given name, returns true, otherwise false 

formData.set(name, value), 

formData.set(name, blob, fileName). 



Sending a form with a file 

Sending a form with a file involves a few extra steps compared to sending a form with only text input fields. You'll need to use FormData to collect the form data, and then use the fetch API to send it to a server. 



Sending a form with Blob data 

ormData objects are used to capture HTML form and submit it using fetch or another network method. 

We can either create new FormData(form) from an HTML form, or create an empty object, and then append fields with methods: 

formData.append(name, value) 

formData.append(name, blob, fileName) 

formData.set(name, value) 

formData.set(name, blob, fileName) 


Two peculiarities here: 

The set method removes fields with the same name, append doesn’t. 

To send a file, 3-argument syntax is needed, the last argument is a file name, that normally is taken from user filesystem for <input type="file">. 

Other methods are: 

formData.delete(name) 

formData.get(name) 

formData.has(name) 



Fetch: Abort 

Step 1: create a controller: 

let controller = new AbortController(); 

A controller is an extremely simple object. It has a single method abort(), and a single property signal. When abort() is called, the abortevent triggers on controller.signal: 

Step 2: pass the signal property to fetch option: 

let controller = new AbortController(); 

fetch(url, { 

  signal: controller.signal 

}); 

Now fetch listens to the signal.  

Step 3: to abort, call controller.abort(): 

controller.abort(); 

We’re done: fetch gets the event from signal and aborts the request. 

AbortController is scalable, it allows to cancel multiple fetches at once. 
