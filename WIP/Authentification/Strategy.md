---
sidebar_position: 1
---

# Authentification Strategy

## Considerations
In order to implement authentication on any website, you have to consider multiple things. Among them are the following:
- The user needs to be able to create an account.
- The user needs to be able to log into their account.
- The server needs to provide the use with a session token after the user logs in.
- The server needs to be able to manage all currently active sessions.
- The server needs to be able to end a session independent of the Client-Side.

We've now broken down the big problem into a lot of little tasks. Lets look at all of them individually and decide on a strategy that takes care of them.


## Backend Strategy
Lets look at the tasks from the scope of the Backend.

### Creating An Account
The steps of creating an account in the Backend are as follows:
1. The Server needs to recieve an account creation request.
1. The request needs to the following things for the Server to create an account:
    - A unique identifier, in our case an **e-mail**.
    - A **password** that proves the user can be associated with the unique identifier.
    - And finally a **display name**. The display name is how other users see the newly created account.
1. The Server needs to validate the user inputs.
    - If they are not valid it should preferrably return an array of validation errors that get displayed to the user.
1. The Server then needs to then hash the password to prevent people with malicious intent to read the passwords in cleartext.
1. The Server needs to now create a separate document that contains user profile information not related to authentification.
    - Bio
    - Profile picture
    - Registration date
    - Characters
    - etc.
1. The final step of the process is, saving the documents to the DB for future reference.

To find out how all of these steps are implemented look at the [Register Account](/docs/Authentification/API/) endpoint's documentation.

### Logging Into An Account
Logging into an account after it has been created is simpler but also contains a lot more caveats. Following things should be considered:
1. The Server needs to recieve a login request.
1. The request needs to contain a unique identifier, in this implementation, an **e-mail**, a **password** and a **session ID**.
1. The Server then needs to find a document in the DB that matches the e-mail and compare the saved password hash with the password provided in the request.
1. If the credentials check out the Server then needs to create a session document and save it to the DB, for future reference. The document needs to contain the following things for future reference in the authenfification process:
    - `session_id`
    - `user_id` A DB reference to the User Object.
    - `expires_at` A IsoDate field that tells the DB when to end (delete) the session.
1. If the credentials don't checkout the Server returns an error that is displayed in the Frontend.
1. Finally the Server sends a user object back to the user containing profile data.


## Frontend Strategy
The things in the Frontend are a lot simpler than in the Backend. The bulk of the Frontend logic consists of making API calls and saving cookies, the only thing that requires extra attention is the *Navigaion Guard* logic. Let's have a look at that.

### Navigation Guard
A *Navigation Guard* makes sure that users cant access any pages that they shouldn't be able to access without authorizing against the API. Let's go through how a *Navigation Guard* works.

Whenever the user navigates to a new page the Frontend checks if the path requires authentification or not. If it does it checks if it is already logged in by checking if a certain cookie exists. If the cookie does not exists it tries to authenticate using it's `session_id`. If the API confirms that no session exists which contains this `session_id`, the user is redirected to the Login page.

In case any of the checks before being redirected to the Login page succeed, the user has a session and is allowed to proceed to the page.























