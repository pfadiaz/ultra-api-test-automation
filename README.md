# Ultra API Postman collection

 <img src="https://www.seleniumacademy.net/wp-content/uploads/2021/06/postman.jpeg" width="400px" height="200px" />

<br>

To use the latest published version , just download the collection file from this repo, then import it into Postman.

### Prerequisites

- You need to have postman installed on your machine

## Usage

The collection will test the `https://gorest.co.in/` REST API, focusing on the CRUD actions of the users endpoint:

```
POST /public/v2/users	Create a new user
GET /public/v2/users/100	Get user details
PUT|PATCH /public/v2/users/100	Update user details
DELETE /public/v2/users/100	Delete user
```

## Tests

This collection contains the following validations done via Postman:

Validate the following positive operations

- "Status Code for sucess requests
- Validate the response body matches the schema expected by the consumer
- Validate value types

"
Validate the following negative operations

- "Status Code for failed requests
- Check how the endpoint handles missing headers / body
- Validate that the endpoint that requires auth does not return data if no auth has been made
- Check error messages and status code when the token has expired"

# Postman Set up

## Steps:

1. Download Postman and sign in with your account
2. Download the collection from this repo located in `./collections/users/`
3. Download the enviroment variables from this repo located in `environment-variables/`
4. Import the collection and the variable file into your Postman workspace, for that please check this out `https://learning.postman.com/docs/getting-started/importing-and-exporting-data/#importing-postman-data`

# Environment Setup

Afte importing the evironment file, from the upper right corner at the top of the screen, click the dropdown and select `staging`. The variables should now be loaded.

# Collection Setup

## Steps:

1. As you can see, the collection has been parameterized with everything. So you don't need to worried about base_urls or test data, like bodies, headers. But, as you know, the request methods:

- PUT
- POST
- PATCH
- DELETE

Will need Authentication. Specifically `Bearer token`. **✋ So, before start ✋**, you need to generate your token from this link:

```
https://gorest.co.in/my-account/access-tokens
```

2. Navigate to that link and login with your prefered email client and that will give you your token.

3. Once you have, copy it
4. Go back to Postman and Select `Staging` as that was name giving to this environment (just for tetsing purposes)
5. Click on the variables icon (eye icon, top right) - and select edit
6. Find the variable `access_token` and paste your token to the current value field.

That is it. You can run the collection by clicking send.

# Execution order:

Postman will run the request in this order:

1. Create a user:
   - Pre-requisite:
     - It will generate a new object with unique data, so everytime a new user is created.Then stores it in a variable.
       Test:
   - Besides the validations, It will extract the userId value and store it in a variable to use them in `create user`, `get user`, `delete user`, `update user`.
2. Get a user - Perform the tests for this endpoint using the userid from the previous step
3. Update a user:
   - Pre-requisite:
     - It will generate a new object with unique data to replace the existing user data, and then check that the update took place.
     - Validate scenarios for this endpoint
4. Finally Delete a user - It will use the userId from step 1 and run the assertions for this request type.

If you need to run any request manually, don'r forget to create the user first. As we need the userId variable to be set.

<br>

# Variables Glossary

| Variable                     | Default value           | Set in      | May override in |
| ---------------------------- | ----------------------- | ----------- | --------------- |
| `access_token`               | -                       | Environment | -               |
| `base_url`                   | `https://gorest.co.in/` | Environment | -               |
| `users`                      | public/v2/users `       | Environment | -               |
| `user_id`                    | -                       | Collection  | Create User     |
| `create_user_request_body`   | -                       | Collection  | Create User     |
| `edit_user_request_body`     | -                       | Collection  | Update User     |
| `existing_user_request_body` | -                       | Collection  | Update User     |
