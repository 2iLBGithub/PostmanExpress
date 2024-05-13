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

---

GET ALL

{yourPort}/beverages / http://localhost:3000/beverages

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response must be an array", function () {
    pm.expect(pm.response.json()).to.be.an('array');
});

pm.test("Array is not empty", function () {
    pm.expect(pm.response.json().length).to.be.above(0);
});

---

GET ONE

{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

TEST

pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("Response has name '{YOUR TERM}'", function () {
    pm.expect(pm.response.json().name).to.eql("{YOUR TERM}");
});

---

POST ONE

{yourPort}/beverages / http://localhost:3000/beverages

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

DELETE ONE

{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

TEST

pm.test("Status code is 204", function () {
    pm.response.to.have.status(204);
});

---

PUT ONE

{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

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

{yourPort}/beverages/{yourNumber} / http://localhost:3000/beverages/1

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

