Purpose
To demonstrate REST functionality on a working server via Postman whilst using some of the tools postman provides, namely collection variables and tests.

Pre-Req
- Have node installed
- Have Postman installed

Steps
- Clone Repo
- npm install 
- node server.js
- import postman file to Postman
- Run the requests

Requests

GET ALL
{yourPort}/beverages / http://localhost:3000/beverages

---

GET ONE
{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

---

POST ONE
{yourPort}/beverages / http://localhost:3000/beverages

Example Body:

{
  "name": "mocha",
  "rating": 6
}

---

DELETE ONE
{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

---

PUT ONE
{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

Example Body:

{
  "name": "nice coffee",
  "rating": 6
}

---

PATCH ONE
{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

Example Body:

{
  "name": "bad coffee"
}
