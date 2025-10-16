# Postman: A Quick, In-Depth Guide (for CS freshmen)

**Names:** Keerthi, Young, Akhil

---

## 1) Introduction
What is an API?  
API stands for Application Programming Interface. It allows for two programs to talk to one another without knowing each other’s internals. It’s like using a restaurant menu; you can see what dishes you can order (the available functions), but you don’t go into the kitchen or need to know how the dishes are made. The kitchen is the inside logic, and the waiter delivering the food is the API.

A more concrete example of this is if you’re building a clothing website, you might not want to deal with all the complex parts of handling credit card payments. Instead, you could use Stripe’s payment API, which takes in your customer’s information, processes it securely, and sends you back a response confirming the payment. This allows you to focus on your store and not on making a reliable payment system.

APIs specify what actions can be taken, what inputs are needed, and what outputs will be returned. For example, a “get user info” API might take a user ID and return the user’s name, email, and address as output in JSON. A weather app doesn’t collect weather data itself; instead, it calls a weather API that provides real-time weather and forecast data.

APIs are everywhere, even when we don’t notice them. When you sign in with Google on a random website, that site is using Google’s OAuth API (the little sign-in using Google button) to authenticate you. When you check your phone’s map or order food, those apps are calling APIs behind the scenes to fetch data from other servers. Once you start to recognize that most software relies on these kinds of interactions, you’ll understand why learning how to use and test APIs is such a foundational skill for computer science students.

---

## REST APIs
One of the most common types of APIs is a REST API (Representational State Transfer). REST APIs use HTTP, which websites also use, to send and receive data. When you make a GET request to something like /users/123, the server returns information about that specific user.

The standard HTTP methods are:
- GET – “get” or retrieve existing data  
- POST – sending data  
- PUT – completely replace existing data  
- PATCH – partially update existing data  
- DELETE – remove data  

REST APIs are stateless, which means that each request contains all the information needed and doesn’t use past requests. This makes them simple, scalable, and easy to debug.

It helps to think of REST APIs as simple conversations. Every request that you send is like asking a question, and each response is an answer. REST’s easy to read format makes it a great starting point for learning about how real-world software systems communicate, especially in web development or mobile app integration.

---

## Common Response Codes
When you send an API request, the server replies with a “status code” that tells you what happened to your request. Here are most of the status codes:

`200 OK` means the request worked successfully.  
`201 Created` means a new resource was successfully created.  
`204 No Content` means the operation worked, but there’s nothing to show in the response.  
`400 Bad Request` means something was wrong with what you sent—often invalid JSON or missing parameters.  
`401 Unauthorized` means you’re not logged in or missing credentials.  
`403 Forbidden` means you’re logged in but don’t have permission to do that action.  
`404 Not Found` means the endpoint or resource doesn’t exist.  
`500 Internal Server Error` means something went wrong on the server’s side.  

Learning to read and interpret these codes is one of the first skills every developer should master when testing APIs. It's okay, you don’t have to memorize them right now, just have them by your side when you use Postman, and over time you will automatically remember what they mean. 

Always read the response body (we will cover this later) along with the code; the body often includes hints or error messages that explain what went wrong and how to fix it.

---

## Why Use Postman
Postman is extremely helpful for working with APIs because it provides a user-friendly interface for sending requests and inspecting responses. You can very easily test whether your endpoints work without needing to write any code. You can store your requests, group them into collections, and even share them with teammates.

Postman will save you time, especially when you’re developing a backend or connecting your app to third-party APIs. Instead of writing scripts to check every endpoint, you can visually test each one with just a few clicks.

For group projects, Postman is also a collaboration tool. You and your teammates can share collections and environment variables so everyone uses the same base URLs, tokens, and request structures. This will make debugging faster and will keep your workflow consistent. In professional settings, entire API teams rely on Postman for testing, documentation, and automation.

---

## Requirements
To use Postman, you’ll need a computer with internet access and the Postman desktop app (available for Windows, macOS, or Linux). A modern browser like Chrome or Firefox helps for checking API documentation. Basic knowledge of JSON and URLs is useful but not required.  
If you’re working with secured APIs, you may also need API keys or tokens. That’s it—once installed, you’re ready to start testing and sending requests.

---

## 2) Installation and Setup
1. Download Postman (desktop app) and sign in (optional, but helps with syncing).  
   https://www.postman.com/downloads/  
   Pick the right download based on your computer’s architecture  

   ![image1](images/image4.png)

2. Once you install it, you will be prompted to sign in. This is not necessary for this tutorial. You can instead select “Switch to Lightweight API Client.”

   ![image2](images/image2.png)

3. Know the layout:  
   Left: Collections (saved requests).  
   Center: Request builder (method, URL, params, headers, body).  
   Bottom/Right: Response (status code, time, size, body, headers).

   ![image3](images/image1.png)

Before testing real APIs, take a moment to explore the interface. Hover over buttons, open tabs, and try switching views. Postman gives you small hints when you hover, and understanding where everything is early on will make you much faster later when troubleshooting or testing larger projects.

---

## 3) Your First GET Request
Let’s start with something simple.

Click “New” → “HTTP Request.”  
Set the method to GET and the URL to https://jsonplaceholder.typicode.com/posts/.  
Click “Send.”  
You’ll see a response with status 200 OK, meaning success. The body will contain data like a post title, user ID, and content.

If you add ?userId=2 to the end of the URL, or use the Params tab to add a key of userId with a value of 2, Postman automatically appends it to the URL. Query parameters like these are used to filter or narrow results in GET requests.

![image4](images/image5.png)

---

## 4) POST Request with JSON
Now send data instead of just reading it.  
Change the method to POST and set the URL to https://jsonplaceholder.typicode.com/posts.

In the Headers tab, add Content-Type as the key and application/json as the value.  
In the Body tab, select “raw,” then choose JSON from the dropdown, and paste:

```json
{
  "title": "Groovy",
  "body": "Groovier",
  "userId": 5
}
```

Click “Send.” If everything is correct, you’ll see status 201 Created and a JSON response showing your data with a new ID field.  
If you see a 400 Bad Request, double-check that your JSON is formatted correctly and that you set the Content-Type header properly.

![image5](images/image3.png)

---

## 5) Headers vs Body vs Params
Use query parameters for filters or searches, headers for metadata (like authentication tokens or content types), and the body for the actual data you’re sending. Knowing when to use each one will help you avoid a lot of errors later on.

---

## 6) Authentication
Most APIs will require you to prove who you are. Common authentication types are:

- API Keys – include something like x-api-key: YOUR_KEY in your headers.  
- Bearer Tokens – usually for OAuth or JWT; the header looks like Authorization: Bearer YOUR_TOKEN.  
- Basic Auth – uses a simple username and password combination that Postman can handle automatically.  

In Postman, go to the Authorization tab and choose the type of authentication, then fill in your credentials.

For security, never hardcode sensitive information. Instead, use Postman’s Environment Variables to store values like {{token}} or {{baseUrl}}.

---

## 7) Troubleshooting
If something doesn’t work:

- Check for typos in your URL or missing slashes.  
- Make sure you’re using the right method (GET vs POST).  
- Validate your JSON structure.  
- Confirm your authentication tokens are current.  
- Use Postman’s console (bottom left) to view detailed logs of requests and responses.

If it works in Postman but not in your web app, it might be a CORS issue—Postman doesn’t enforce browser restrictions, but browsers do.

---

## 8) Building Good Habits
Always name your requests clearly (like [GET] /users/:id or [POST] /auth/login). Add a short description explaining what each one does. Save everything in a collection and test your responses regularly. You can even write small “tests” in Postman to automatically check whether your API returned a 200 status or contains a certain JSON key.

---

## 9) Summary
Postman is one of the most powerful yet beginner-friendly tools you’ll ever use as a developer. It simplifies API testing, debugging, and learning. Once you’re comfortable with GET and POST requests, you can experiment with more advanced features like mock servers, automated testing, and documentation generation.

Learning to use Postman effectively will help you not only in your CS classes but also in internships and real-world projects. You’ll gain a better understanding of how front-end and back-end systems communicate, and more importantly, how to verify that everything actually works before your users ever see it.
