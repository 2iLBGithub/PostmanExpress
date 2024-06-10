Purpose
To demonstrate REST functionality on a working server via Postman whilst using some of the tools postman provides, namely collection variables and tests.

Summary
This repository focuses mainly on providing an express server with logic for REST operations. It also has a data.json file where an object, beverages, with a list of said beverages, is stored. We can therefore use Postman to interact with this server and its supporting data.json, and when we make these requests we can also run tests.

Pre-Req
- Have node installed
- Have Postman installed

Steps
- Clone Repo
- npm install shouldn't be necessary as the modules are already in the repository, but if problems abound the first step would be to delete the modules, package-lock.json and install
- node server.js
- Import postman file to Postman
- Run the requests

Requests
The requests are split into two sections each, namely the request and the tests which accompany it. Note that each request and test interacts with the data.json file in the express server, and as such some requests and tests may fail if requests overlap, ie if one was to delete with id = 1 and was then to attempt a put/patch on the same item. 

---

GET ALL

{yourPort}/beverages OR http://localhost:3000/beverages

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("'beverages' key contains an array", function () {
    var responseData = pm.response.json();
    pm.expect(responseData.beverages).to.be.an('array');
});

pm.test("Array is not empty", function () {
    var responseData = pm.response.json();
    pm.expect(responseData.beverages.length).to.be.above(0);
});

---

GET ONE

{yourPort}/beverages/{yourNumber} OR http://localhost:3000/beverages/1

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has name '{YOUR TERM}'", function () {
    pm.expect(pm.response.json().name).to.eql("{YOUR TERM}");
});

---

POST ONE

{yourPort}/beverages OR http://localhost:3000/beverages

Example Body:

{
  "name": "mocha",
  "rating": 6
}

TEST

pm.test("Status code is 201", function () {
    pm.response.to.have.status(201);
});

pm.test("Response has correct name and rating", function () {
    var resp = pm.response.json();
    pm.expect(resp.name).to.eql("mocha");
    pm.expect(resp.rating).to.equal(6);
});

---

PUT ONE

{yourPort}/beverages/{yourNumber} OR http://localhost:3000/beverages/1

Example Body:

{
  "name": "nice coffee",
  "rating": 6
}

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has updated values", function () {
    var resp = pm.response.json();
    pm.expect(resp.name).to.eql("nice coffee");
    pm.expect(resp.rating).to.equal(6);
});

---

PATCH ONE

{yourPort}/beverages/{yourNumber} OR http://localhost:3000/beverages/1

Example Body:

{
  "name": "bad coffee"
}

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Name has been updated to 'bad coffee'", function () {
    pm.expect(pm.response.json().name).to.eql("bad coffee");
});

---

DELETE ONE

{yourPort}/beverages/{yourNumber} OR http://localhost:3000/beverages/1

TEST

pm.test("Status code is 204", function () {
    pm.response.to.have.status(204);
});

---
