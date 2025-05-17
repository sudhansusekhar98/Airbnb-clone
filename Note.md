* SHOW ROUTE
//validate our schema
    /* 
      if (!listing) {
        throw new ExpressError(400, "Send a valid data for listing");
      }
  
      if(!newListing.title){
          throw new ExpressError(400, "Title is missing!");
      }
      if(!newListing.description){
          throw new ExpressError(400, "Description is missing!");
      }
      if(!newListing.location){
          throw new ExpressError(400, "Location is missing!");
      } */
    //To avoid using multiple if conditions we need to add the joi to validate the Schema


// app.get('/login', (req, res) => {
// res.render('listings/login.ejs', { error: null }); // make sure to match folder path
// });

// app.post('/login', (req, res) => {
// const { email, password } = req.body;

// if (email === 'test@wanderlust.com' && password === 'password123') {
// res.redirect('/listings');
// } else {
// res.render('listings/login.ejs', { error: 'Invalid email or password.' });
// }
// });

// app.get('/testlisting', async (req, res)=>{
// let sampleListing = new Listing({
// title: 'My New Villa',
// description: "At the beach",
// price: 1200,
// location: 'Goa',
// country: 'India'
// })

// await sampleListing.save();
// console.log("Sample was saved");
// res.send("successful testing");
// })

- CookieParser

const cookieParser = require("cookie-parser");

cookie-parser is a middleware in Express used to parse cookies from the HTTP request headers and make them easily accessible in your app.

app.use(cookieParser("secretcode"));

app.get('/getsignedcookie', (req, res)=>{
res.cookie("made-in", "USA", {signed: true});
res.send("done!")
});

app.get('/verify', (req, res)=>{
let reqCookies = req.signedCookies;
console.log(reqCookies);
res.send('verified');
})

app.get("/getcookies", (req, res) => {
res.cookie("greet", "hello");
res.cookie("MadeIn", "India");
res.cookie("name", "Sourav")
res.send("sent you some cookies.");
});

app.get("/", (req, res) => {
console.dir(req.cookies);
res.send("Hi, I am root!");
});

app.get("/greet", (req, res) => {
let { name = 'anonymous' } = req.cookies;
res.send(`Hello, ${name}`);
});

session
express session: An attempt to make our session stateful
const session = require("express-session");

app.use(
session({
secret: "mysupersecretstring",
//This will create a new session and assign a session ID to a client if they don’t already have one, and store that ID in a cookie for future requests.
// Used to sign the session ID cookie — keep this secure and ideally in environment variables.
resave: false,
saveUninitialized: true,
})
);

app.get("/reqcount", (req, res) => {
if (req.session.count) {
//req.session tracks the single session
req.session.count++;
} else {
req.session.count = 1;
}
res.send(`you sent a request ${req.session.count} times!`);
});

This image explains how passwords are **stored securely** using **hashing**:

### Key Points:

* **Plain passwords are never stored.**

  * Example: Instead of saving `"helloworld"`, we store a **hashed version**.
* **Hashing Function**:

  * Takes the plain password and converts it into a unique, fixed-length string (the hash).
  * Example Hash:
    `936abc...b6f8f8f07af`
    (This is just a sample; actual hash length and content depends on the algorithm used.)

### Process:

1. During **signup**, the user provides:

   * Email
   * Username
   * Password
2. The password goes through a **hashing function**.
3. Only the resulting **hashed password** is stored in the database — not the original password.

### Why Hashing is Important:

* It protects users’ passwords in case of a data breach.
* Even if someone gets access to the database, they can't easily reverse the hash to get the original password.

Let me know if you want code examples for hashing passwords using libraries like **bcrypt** or **argon2** in Node.js or any other language.

## Hashing
What we need to know?

For every input, there is a fixed output

They are one-way functions, we can’t get input from output

For a different input, there is a different output but of same length

Small changes in input should bring large changes in output

## Salting

Password salting is a technique to protect passwords stored in databases by adding a string of 32 or more characters and then hashing them.

## Configuring Strategy
passport.initialize()
A middleware that initializes passport.

passport.session()
A web application needs the ability to identify users as they browse from page to page. This series of requests and responses, each associated with the same user, is known as a session.

passport.use(new LocalStrategy(User.authenticate()))

## understanding of passport tool


## MVC: Model, View, Controller

Implement Design Pattern for Listings 
Storing core backend logic in controllers is a common and effective way to organize and compact your code, especially in MVC (Model-View-Controller) or similar architectural patterns.