
# API Testing

## What is API really?
- Mechanisms that enable two software components to communite with each other using a set of definations and protocol
- API --> Application Programming Interface. Application is software and Interface depicts that two software are communicating with req and res. API documentation defines how that req and res structured

## How do API's work
- Follows client-server architecture
- Four different api's
	- SOAP API
		- Simple Object Access Protocol.
		- Client and server exchagnes messages using XML

	- RPC API
		- Remote Procedure Calls
		- Client complete work on server and server responds back with output
	- Websocket APIs
		- Modern web API uses json objects to pass data
		- Supports two way communication between client and server & server can send callbacks to client
	
	- REST APIs
		- Representational State Transfer 
		- Client send request to server with data
		- Server process it and responds with output
		- Widely used and most popular API
		- Uses set of functions like GET, PUT, DELETE, POST
		- Stateless protocol uses HTTP and HTTPS for exchanging data


------

# API recon
- Find API endpoints --> hwere API recieves request for a specific resources
![alt text](/API_testing/Images/image.png)
- API endpoint for this request is `/api/books`. The result will be the software as the server will retrieve the books list and send it to client via API
- After identifying the endpoint, Need to determine how to interact with them
- This allows you to contruct valid HTTP request
- Find these info also:
	- Input data the API processes, including both compulsory and optional parameters
	- The types of requests API appects accepts, including supported HTTP methods and media formats
	- Rate limits and authentication 

# API Documentation
- APIs are usually documented so that developers know how to use and integrate with them. 
- Documentation is both human and machine readable
- Machine readable documentation is designed to be processed by a software for automating tasks like API Integration and validation
- Written in Json or XML
- API documentation is publicly available, paritcularly if the API is intended for use by external developers

## Dicovering API documentation

request fuzzing tool can help finding API documentation even if its not openly available

- Potential endpoint 
	- `/api`
	- `/swagger/index.html`
	- `/openapi.json`

- Investigate each api endpoint deeeper

# Exercise 1 

To solve the lab, find the exposed API documentation and delete carlos. You can log in to your own account using the following credentials: wiener:peter. 

1. Configure foxyproxy and burpsuite
2. Log in your account using given credentials --> `wiener:peter`
3. Refresh browser while keep intercept on in burp
4. Catch request and sent to repeater
5. Search for common api endpoints 
![alt text](/API_testing/Images/image-1.png)

There, we can see the api documentation and endpoints for performing operations such as retrieving user info and deleting user
![alt text](/API_testing/Images/image-2.png)

6. Let see if we can retrieve target (carlos) account info

![alt text](/API_testing/Images/image-3.png)

7. Now.Sent the request to `/api/user/carlos` with `DELETE` as HTTP METHOD
![alt text](/API_testing/Images/image-4.png)

Solved !!!!

---

Take the discovered machine 
readable documentation and put it through  range of automated tools to analyze it --> Postman or SoapUI

# Identifying API endpoints
- Check for the common api endpoints `/api`
- Check for javascript files as they may contain references to API endpoints

# Interacting with API endpoints
- Repeated interaction to find how data is being handled by API
- Reviewing error messages and other responses, allowing us to construct valid HTTP request

## Identifying Supported HTTP methods

HTTP method specifies the action to be performed on resource :
- `GET` --> Retrieves data from resources
- `PATCH` --> Applies partial changes to resources
- `OPTIONS` --> Retrieves information on types of reqeust methods can be used on that resource

## Identifying supported content types
- API endpoints expect data in specific format and behave differently on content type of the data provided in request
	- Trigger errors that disclose useful informaiton
	- Bypass flawed defenses
	- Take advantage of differences in processing logic
	- API may be secure when handling JSON data but susceptible to injection attacks when dealing with XML

---
# Exercise 2
To solve the lab, exploit a hidden API endpoint to buy a Lightweight l33t Leather Jacket. You can log in to your own account using the following credentials: wiener:peter

1. Login your account with given credentials
2. Head over to home --> lightwieght leather and while interpecting add the jacket to the cart
3. Got the request to `/api/product/1/price`
![alt text](/API_testing/Images/image-5.png)

4. Seems to handling json data lets try to read documentation if we can find or cut down the api uri and read it one by one
![alt text](/API_testing/Images/image-6.png)

Same message in all

5. Lets see what method does it accepts
![alt text](/API_testing/Images/image-7.png)

6. Seems like only GET and PATCH are supportive and with PATCH the content-type must be `application/json` so lets make the changes and observe again

![alt text](/API_testing/Images/image-8.png)

7. Found a breaking point, since its parse json lets try and give it some json data and we know PATCH method also make partial changes so 

![alt text](/API_testing/Images/image-9.png)

8. Lets give it parameters and play with some values 


![alt text](/API_testing/Images/image-10.png)

9. Now jump back to home page --> refresh --> jacket with $0.00 and checkout


Bingoo!!!! we got a jacket for free

Solved !!!

---
