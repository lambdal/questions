# Create a sign up form

**Hint:** Simple is better. Don't feel bad if your submission is simply one JS file, one HTML file, and one CSS file.

For this take-home assignment, you will be creating a sign up form. The form will have the following fields:

- First name
- Last name
- Email
- Password

Before getting started, clone this repository,The sign up form should look and behave similar to the form served at `localhost:5000`

The backend server can be run locally after cloning this repository and running the following command:
```
flask --app backend run
```

![Twilio sign-up form](https://i.imgur.com/eZERbKy.png)

The goal is to emulate the behavior of Twilio's form as closely as possible. We recommend you spend some time playing around it. Pay attention to how it provides timely validation to user input. **Note:** See how Twilio handles an already-registered emai using`m@lambdal.com`.

## Requirements
* Your code should perform client-side validation and display errors when applicable. Specifically, ensure that:
   * `first_name` is a string of at least two characters
   * `last_name` is a string of at least two characters
   * `email` is not already registered and a string that looks like an email (just write a basic sanity check)
   * `phone` is string composed of 10 numerical characters, not starting with a zero
* The form should look & behave similarly to Twilio. For example:
   *  Focusing on an input element should lift and shrink its placeholder text and change its the underline color
   *  Unfocusing on an input field should trigger validation
* The form should submit its data to a locally running backend server (see below) and display any errors it returns.

**Special phone number**
Let's assume that the user fills out the form using a valid, available email and valid first name, last name, and phone.


## Backend endpoints

### Check if an email is taken
```
POST http://localhost:5000/api/is-email-taken
```
##### Request format
```
{
    "email": <an email address>
}
```

##### Response
The backend will return a JSON object that lets you know if the email address is taken.
```
{
    "is_taken": [true|false],
}
```

##### Special inputs
- email: `m@lambdal.com` will be considered taken

### Register a user
```
POST http://localhost:5000/api/is-email-taken
```

##### Request format
```
{
    "first_name": <a string, at least two character>,
    "last_name": <a string, at least two character>,
    "email": <a string that looks like an email>,
    "phone": <a string composed of 10 numerical characters, not starting with "0">
}
```
##### Response

The backend will validate input, including an additional check on whether the
email is already registered. If the input is valid, the HTTP response will be
status 200 and return a JSON object that looks like this:

```
{"errors": {"first_name": None,
            "last_name": None",
            "email": None,
            "phone": None}}
```

If the input fails validation, the HTTP response will be status 400 and look something like this:

```
{"errors": {"first_name": "That doesn't look like a first name",
            "last_name": None",
            "email": "That email is taken",
            "phone": None}}
```

##### Special inputs
- email: `takenemail@gmail.com` (to simulate a taken phone number)
- phone: 7777777777 (to simulate an unreachable phone number)


## Running the local backend server
The backend server can be run locally after cloning this repository and running the following command:
```
flask --app backend run
```
## What technologies to use
Whatever you want. We recommend using a framework like React/Angular/Vue.js to make your life easier. If you don't like CSS, feel free to use something like Sass.

## How to submit
Email your answer to your recruiter (e.g. your .js, .css, .html files). Include instructions for running your form in a browser - for example, if it's written in a non-JS framework, describe how to compile it.
