# API Testing Labs

## Lab 1 — Exploiting an API endpoint using documentation
 
### Introduction
* This lab explains about
  1. API testing
  2. API recon
  3. API documentation
* Has a practical Lab

### What i learned 

#### 1.API testing
* APIs (Application Programming Interfaces) allows systems and application to communicate and share data
* All dynamic website are composed of APIs so testing them is important because it can compromise the CIA traids

#### 2. API recon
* Before we start testing we need to find as much as information about the API , we should identify endpoints
* On endpoints API gets a request about a specific resource on its server
* Once we identify the end point we need to know how to connect with them to send a successful http request
* We should find out about the input data the API process, the type of requests, rate limits

#### 3. API documentation
* Developers usually document API's they might be human-readable and machine-readable
* API's written structure formats like JSON or XML
* Most of the time API documentation isn't available but by crawling the API using Burp Scanner we can find one
* We can also use a list of common paths
* As i mentioned earlier API documentation is either human readable or machine readable , using machine readable documentation we can use tools to analyze them
* Tools like postman or soapUI are used to test document endpoint

#### 4.Lab
* The lab askes as to login using credentials (wiener:peter), find the exposed API and remove or delete carlos
* To solve this lab we need to know what API documentation is and how to discover API documentation
* I started by logging in  into the account by using the credential i was given and then it gave a blank space to update wiener's email i updated to test@gmail.com
* As i said earlier to solve this lab we need to have a great knowledge about API and how we can get the API file the method i used was add /api at the end of the URL  like this
  https://0ad40006036a92f680d4e4a0006900fe.web-security-academy.net/api
* Now i got the REST API and The documented REST API defines three operations for managing user resources on the lab we were asked to DELETE Carlos
* we hit the delete operation it will ask us to submit a username : string* we were asked to delete Carlos so we enter Carlos's name and we send a request and Carlos is deleted

## Lab 2: Finding and exploiting an unused API endpoint

### Introduction
* This lab explains about
  1.Identifying API endpoints
  2.Interacting with API endpoints
  3.Identifying supported HTTP methods and Identifying supported content types
* Has a practical Lab

### What i learned 

#### 1.Identifying API endpoints
* Even if we have API documentation we can also gather information by using the application that uses the API we do this because sometimes documents might be outdated or in accurate
* We can also use Burp Scanner to sniff then manually investigate interesting attack surface using the Burp's browser
* While browsing we can look for patterns like /api/ and also one thing that might help us even trigger API endpoints is JavaScript file we can study the file in two ways the first one is just manually reviewing it and the other one is using JS Link Finder BApp

#### 2.Interacting with API endpoints
* After identifying the API end points we can interact with them using Burp Repeater and Burp Intruder
* When we interact with them using Burp it will enable us to observe the API behavior
* Lets say we are interacting with API endpoint we will got error messages and other responses we should monitor them closely because they might give us clue or insight on how to construct a valid HTTP request.

#### 3.Identifying supported HTTP methods and Identifying supported content types
* The HTTP method specifies the action to be performed on the resource like
    1. GET : retrieve / get data from the resource
          example : GET /api/tasks
    2. PATCH : apply change to a resource
          example : POST /api/tasks
    3. OPTIONS : it askes what method is allowed example finding out if GET, POST, PATCH etc are                            supported
 * It would be exhausting to cycle every single method so we could use the build-in _HTTP verbs_ in Burp     intruder
   > **One thing to note when testing HTTP methods is that we need to test them on resource that has low         priority because they might destroy the whole record for example DELETE /users/1 might actually           delete user number 1**
* Usually API endpoints expect data in a specific format so when we change the methods they might behave differently so changing the content type might enable us
    1. Trigger errors that might give us useful information
    2. we might find our way around the security protection
    3. depending on the format the program might treat two things differently like the developer might           security JSON and forgot to do the same for XML
 
 #### 4.Lab
 * To solve this lab we need to exploit a hidden API endpoints to buy **Lightweight l33t Leather Jacket**    we can login as we did on the first lab
 * What i did was first i logged into my account using my credentials and updated the email to my test@gmail.com
 * On the home page we got the **Lightweight l33t Leather Jacket** we click on it add it our cart
 * We go to the cart page and we place our order when we do that it will tell us the we cant purchase it but we want it so bad so what we will do is that make the price 0 so we can afford it
 * We go to the jackets page and we inspect the page we got network change the GET method to POST request and add application/json on the header and on body we do {"price":"0.00"}
 * Click the blue Send button at the bottom. Navigate to or refresh the Cart page in the browser to verify the jacket was added at $0.00.

## Lab 3: Exploiting a mass assignment vulnerability

### Introduction
* This lab explains about
  1. Using Intruder to find hidden endpoints
  2. Finding hidden parameters
  3. Mass assignment vulnerabilities , Identifying hidden parameters , Testing mass assignment                 vulnerabilities
  4. Preventing vulnerability in APIs
* Has a practical Lab

### What i learned 
####  1. Using Intruder to find hidden endpoints
*  When developer build API they usually follow predictable RESTful structure
*  If we find a working endpoint there is a high probability we might find other endpoint
*  Another tip is when looking for hidden endpoint its better to use wordlists based on common API naming
  
####  2. Finding hidden parameters
* Another way to change the application behavior might be when we are doing API recon we might find undocumented parameters the the API takes we can use them
* Burp tools that's used in identifying hidden parameter
   1. Burp Intruder: : Automatically tests many different parameter names in a GET query string
   2. Param Miner (Burp Extension): A tool for high-speed discovery of hidden parameters.
   3. Content Discovery: Finding hidden website resources and endpoints that aren't directly linked.
      
#### 3. Mass assignment vulnerabilities , Identifying hidden parameters , Testing mass assignment                 vulnerabilities
* Mass assignment (also called auto-binding) happens when an application automatically takes parameters from a request and puts them into an internal object.
* It might even make the application to use hidden parameter that the developer never intended the user to use
* We might often find hidden parameters by looking carefully at the the data
* To test whether you can modify the enumerated isAdmin parameter value, add it to the PATCH request

#### 4. Preventing vulnerability in APIs
* when we design API's we need to make it secured by doing the following
  1. we can make our API documentation private
  2. keep the API documentation up to date
  3. on the http method do an allow list
  4. don't make the errors to reveal to much information
  5. secure everything equally especially on every version of the API 

#### 4 Lab
* To solve the lab we need to  find and exploit a mass assignment vulnerability to buy a Lightweight l33t Leather Jacket
* We can login using the last credential we used
* First thing we do is find the hidden parameter to get that we look at the response form which is GET /api/checkout
* On the response we saw a strange code which says 
```
"chosen_discount": {
    "percentage": 0
}
```
* This code is strange because we don't normally control chosen_discount this gave us an idea even though it wont let us edit it on the front we might still find a way to modify it
* What we do next is find the request that create the order in the HTTP history POST /api/checkout earlier we say the chosen_discount might be modified so what if we add it here on , also in here we find this code
 ```
  {
  "chosen_products": [
    {
      "product_id": "1",
      "quantity": 1
    }
  ]
}
 ```
* In the codes the main vulnerability is it accept a filed even though the user shouldn't have been allowed to manipulate it , to modify we just add and send the request
```
  "chosen_discount": {
    "percentage": 100
}
  ```
* The server response with HTTP/2 201 Created , 201 created mean the server successfully created something and we got the successful response which is /cart/order_confirmation?order-confirmed=true
* Now when we refresh the lab we got the message that we finished the lab
  






