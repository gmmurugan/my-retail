###### CaseStudy  | **myRetail RESTful service**

           myRetail is a rapidly growing company with HQ in Richmond, VA and over 200 stores across the east coast. myRetail wants to make its internal data available to any number of client devices, from myRetail.com to native mobile apps. 
    The goal for this exercise is to create an end-to-end Proof-of-Concept for a products API, which will aggregate product data from multiple sources and return it as JSON to the caller. 
    Your goal is to create a RESTful service that can retrieve product and price details by ID. The URL structure is up to you to define, but try to follow some sort of logical convention.
    Build an application that performs the following actions: 
    Responds to an HTTP GET request at /products/{id} and delivers product data as JSON (where {id} will be a number. 
    Example product IDs: 15117729, 16483589, 16696652, 16752456, 15643793) 
    Example response: {"id":13860428,"name":"The Big Lebowski (Blu-ray) (Widescreen)","current_price":{"value": 13.49,"currency_code":"USD"}}
    Performs an HTTP GET to retrieve the product name from an external API. (For this exercise the data will come from redsky.target.com, but let’s just pretend this is an internal resource hosted by myRetail)  
    Example: http://redsky.target.com/v2/pdp/tcin/13860428?excludes=taxonomy,price,promotion,bulk_ship,rating_and_review_reviews,rating_and_review_statistics,question_answer_statistics
    Reads pricing information from a NoSQL data store and combines it with the product id and name from the HTTP request into a single response.  
    BONUS: Accepts an HTTP PUT request at the same path (/products/{id}), containing a JSON request body similar to the GET response, and updates the product’s price in the data store._  
    
**Tech Stack**
_____

`Java:1.8 |
SpringBoot:Latest |
JUnit | 
Python |
MongoDB | 
Docker`

Dev
$ git clone https://github.com/gmmurugan/casestudy/my-retail.git
$ cd <workspace>/code/my-retail

$ docker-compose up
    you could bring up local mongodb and seed the db. refer products.json and seed_mongo.py for importing few documents
    -- brew install mongodb
    -- brew services start mongodb // hope i dont need to document these things :-)
    -- use mongocompass to create db and collection name
    -- pip install pymongo && python ./seed_mongo.py
Tests
Integration tests needs a MongoDB local/docker.

Make sure the docker images are running by using:
$ docker-compose up

API's
GET http://localhost:8080/product/13043945 HTTP/1.1
Content-Type: application/json

use REST Client to test the PUT API

PUT http://localhost:8080/product/13043945 HTTP/1.1
Content-Type: application/json

{
"id": 456,
"price": {
"value": 11.99,
"currency_code": "USD"
}
}

Production Readiness
 I have explored multiple serverless options to build this REST API and pretty much i ended up with few compatibility with the 
data structure we have. However, its dockerized and any cloud could take this with proper testing and pipeline setup

Scalability - Yes
 
