# Files-Patterns-and-Flags-in-JavaScript

## Table of Contents

- [File Objects ](#File-Objects )
- [FormData](#FormData)
- [Fetch: Cross-Origin Requests ](#Fetch:-Cross-Origin-Requests )
- [Patterns and Flags](#Patterns-and-Flags)


## File-Objects
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



## Fetch:-Cross-Origin-Requests

Cross-origin requests, also known as CORS (Cross-Origin Resource Sharing), refer to web page requests made from one domain (origin) to another domain. By default, web browsers enforce a security policy known as the same-origin policy, which restricts web pages from making requests to a different domain than the one the page came from. 

CORS is a security feature implemented by web browsers to control which web pages are allowed to access resources (like data, scripts, or fonts) on a web page from a different domain. It is crucial for web security, as it prevents malicious scripts from making unauthorized requests on behalf of a user. 

To allow cross-origin requests, the server hosting the resource can include specific HTTP headers in its response to indicate which domains are permitted to access the resource. These headers include: 

Access-Control-Allow-Origin: This header specifies which domains are allowed to access the resource. For example, if a server sets this header to Access-Control-Allow-Origin: example.com, then only pages from example.com are allowed to make requests. 

Access-Control-Allow-Methods: This header indicates which HTTP methods (GET, POST, PUT, DELETE, etc.) are allowed when making a cross-origin request. 

Access-Control-Allow-Headers: This header specifies which HTTP headers are allowed in a request. 

Access-Control-Allow-Credentials: This header indicates whether credentials (like cookies or HTTP authentication) can be included in a cross-origin request. 

Access-Control-Max-Age: This header specifies how long the response to a preflight request (an initial request made by the browser to check if the full request is allowed) can be cached. 

Access-Control-Expose-Headers: This header allows servers to specify which headers can be exposed to the response. 

CORS is an essential security feature, as it prevents unauthorized access to sensitive resources. However, it can sometimes be a challenge for web developers when they need to make requests from different domains. They might need to configure their server to include the necessary CORS headers or use techniques like JSONP or server proxies to work around the restrictions. 

 

 

Using Forms 

One way to communicate with another server was to submit a <form> there. People submitted it into <iframe>, just to stay on the current page, like this:  

  

So, it was possible to make a GET/POST request to another site, even without networking methods, as forms can send data anywhere. But as it’s forbidden to access the content of an <iframe> from another site, it wasn’t possible to read the response.  

To be precise, there were actually tricks for that, they required special scripts at both the iframe and the page. So the communication with the iframe was technically possible. Right now there’s no point to go into details, let these dinosaurs rest in peace.  

Simple Requests 

A simple request is a request that satisfies two conditions: 

Simple method: GET, POST or HEAD 

Simple headers – the only allowed custom headers are: 

Accept, 
Accept-Language, 
Content-Language, 
Content-Type with the value application/x-www-form-urlencoded, multipart/form-data or text/plain. 

CORS for Simple Requests 

CORS (Cross-Origin Resource Sharing) is a security feature implemented by web browsers to control which web pages are allowed to access resources (like data, scripts, or fonts) on a web page from a different domain. There are two types of requests in CORS: Simple Requests and Preflighted Requests. 

Let's focus on Simple Requests first: 

Simple Requests: 

A request is considered a "simple request" if it meets the following conditions: 

It uses only the following methods: 

GET 

HEAD 

POST 

The only allowed request headers are: 

Accept 

Accept-Language 

Content-Language 

Content-Type (with a value of application/x-www-form-urlencoded, multipart/form-data, or text/plain) 

The only allowed Content-Type in the request entity body is: 

text/plain 

multipart/form-data 

application/x-www-form-urlencoded 

No event listeners are registered on any XMLHttpRequestUpload object used in the request (for example, progress event listeners). 

If a request meets all these criteria, it's considered a Simple Request. 

CORS Handling for Simple Requests: 

For Simple Requests, the browser adds an Origin header to the request indicating the origin of the page making the request. 

If the server's response includes the appropriate CORS headers, and the origin is allowed, the browser allows the request to go through. The relevant headers include: 

Access-Control-Allow-Origin: This header specifies which domains are allowed to access the resource. For a Simple Request, it can be set to * (allowing any origin) or a specific domain. 

Access-Control-Allow-Methods: This header indicates which HTTP methods (GET, POST, PUT, DELETE, etc.) are allowed when making a cross-origin request. 

Access-Control-Allow-Headers: This header specifies which HTTP headers are allowed in a request. 

Access-Control-Allow-Credentials: This header indicates whether credentials (like cookies or HTTP authentication) can be included in a cross-origin request. 

Access-Control-Max-Age: This header specifies how long the response to a preflight request (an initial request made by the browser to check if the full request is allowed) can be cached. 

Simple Requests don't require a preflight request (OPTIONS request) to be sent by the browser before the actual request. The browser directly sends the request, and the server responds with the appropriate CORS headers. 

 

Non-simple Requests 

There are a few things that can make a request non-simple:  

Different Actions: If the web page is trying to do something more complex, like changing information or adding new things, it's considered a non-simple request.  

Custom Settings: If the request is using special settings or asking for special information, it's also considered non-simple.  

Checking Permission: When a non-simple request happens, the browser sometimes checks with the other website to make sure it's allowed to do the special thing. This is like asking for permission before doing something important. 

 
Credentials 

In the context of web development and CORS (Cross-Origin Resource Sharing), "credentials" refer to sensitive information that can be used to authenticate a user or establish a session. This typically includes cookies, HTTP authentication, and client-side certificates. 

When making cross-origin requests, browsers have a security feature that restricts whether or not credentials (like cookies) can be sent along with the request. This is important for security because it prevents unauthorized sites from making requests on behalf of a user. 

There are two levels of credentials that can be sent with a request: 

Same-origin requests: 

For requests made to the same domain (origin), cookies and other credentials are sent by default, assuming the server has set appropriate Set-Cookie headers. 

In this case, the browser automatically includes cookies associated with the domain. 

Cross-origin requests: 

For requests made to a different domain, credentials are not sent by default. This is a security measure to prevent unauthorized access. 

If you want to send credentials with a cross-origin request, you need to set the withCredentials property of the XMLHttpRequest object (or use the credentials option in Fetch API) to true. 

Additionally, the server must include the Access-Control-Allow-Credentials header in its response with a value of true. 


## Patterns-and-Flags

A regular expression (also “regexp”, or just “reg”) consists of a pattern and optional flags. 

patterns and flags typically refer to regular expressions (regex) and their associated flags. Regular expressions are a powerful tool for matching patterns in strings. 


Usage 

Validation: Email Addresses: Regex can be used to validate email addresses. 

Search and Replace: You can use regex for pattern-based search and replace operations. 

Parsing: Regex can be used to extract specific information from strings. 

Password Strength: You can use regex to enforce password strength requirements. 

Data Extraction: Parsing data from structured text, like logs or CSV files. 

URL Routing: In web applications, regex can be used for handling route matching. 

Data Cleaning: Removing unwanted characters or formatting from text. 


Flags 

Regular expressions may have flags that affect the search. 

There are only 6 of them in JavaScript: 

I (Case-Insensitive) With this flag the search is case-insensitive: no difference between A and a (see the example below). 

G (Global) With this flag the search looks for all matches, without it – only the first one  

M (Multi-line) Multiline mode (covered in the chapter Multiline mode, flag "m"). 

S (DotAll) “Dotall” mode, allows . to match newlines (covered in the chapter Character classes). 

U (Unicode) Enables full unicode support. The flag enables correct processing of surrogate pairs. More about that in the chapter  Unicode: flag "u". 

Y Sticky mode (covered in the chapter Sticky flag "y", searching at position) 


Character classes 

In regular expressions, character classes allow you to match a set of characters rather than just a single character. They are denoted by square brackets [ ]. 

When the pattern contains \b, it tests that the position in string is a word boundary, that is one of three variants: 

Immediately before is \w, and immediately after – not \w, or vise versa. 

At string start, and the first string character is \w. 

At string end, and the last string character is \w. 

Inverse Classes 

An inverse class, also known as a negated character class, allows you to match any character except those listed within the class. In regular expressions, you can create an inverse class by using the caret (^) symbol as the first character inside the square brackets ([]). 

For example: 

[^abc] matches any character that is not a, b, or c 

The “reverse” means that it matches all other characters, for instance: 

\D 

Non-digit: any character except \d, for instance a letter. 

\S 

Non-space: any character except \s, for instance a letter. 

\W 

Non-wordly character: anything but \w. 

\B 

Non-boundary: a test reverse to \b. 


Escaping, Special characters 

In regular expressions, certain characters have special meanings and are used to perform specific operations. To match these characters literally, you need to "escape" them using a backslash (\). 

(Dot) In regex, . matches any single character except for a newline character. To match a literal dot, you need to escape it. 

(Asterisk): In regex, * matches zero or more occurrences of the preceding character or group. To match a literal asterisk, you need to escape it. 

+ (Plus): In regex, + matches one or more occurrences of the preceding character or group. To match a literal plus sign, you need to escape it. 

? (Question Mark): In regex, ? matches zero or one occurrence of the preceding character or group. To match a literal question mark, you need to escape it. 

[] (Square Brackets): Square brackets are used to define character classes in regex. To match a literal square bracket, you need to escape them. 

\ (Backslash): The backslash itself is a special character in regex. To match a literal backslash, you need to escape it. 

 
