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
* 
