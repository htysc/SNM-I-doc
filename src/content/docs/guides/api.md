---
title: API
---

These are the internal APIs between the frontend and backend (see [project architecture](/project-structure/#architecture)).
You can find their implementations in `backend/services/` and
their corresponding routes in `backend/routes/`.

**All API routes below are prepended with `/api/`.**

## `backend/routes/base.js`
This section refers to the [User-related Functionality section of the business requirement](https://docs.google.com/document/d/1apQqxKiYnGoXbPFWx7PguT-G1Su_SuZkOwM22ZZHEEE/edit#heading=h.5kzbh922oce3).
Particularly the ability to log in and out of the application.

Route | Method | Parameters | Action | Return
---|---|---|---|---
`login` | POST | email<br>password | Check the password and email and set the backend to logged in state | user account info
`login/securityQuestions/fetch` | GET | user id | | user's primary email and security questions
`login/securityQuestions/check` | POST | primary email<br>security question<br>answer | Check if the answer is correct | success
`logout` | POST | | Logs out of the session |

## `backend/routes/register.js`
This section refers to the [User-related Functionality section of the business requirement](https://docs.google.com/document/d/1apQqxKiYnGoXbPFWx7PguT-G1Su_SuZkOwM22ZZHEEE/edit#heading=h.5kzbh922oce3).
Particularly the ability to register with the application.

Route | Method | Parameters | Action
---|---|---|---
`register/invite` | POST | email<br>superuser flag<br>expiration date | Create a temporary user and sends an email with the invitation link
`register/firstEntry/verify` | POST | jwt token (sent with the invitation email) | Check if the token was sent within 24 hours and not used already
`register/firstEntry/update` | PUT | email<br>password<br>security questions | Update the user with the provided info and set the user from temporary to permanent

## `backend/routes/user.js`
This section refers to the [User-related Functionality section of the business requirement](https://docs.google.com/document/d/1apQqxKiYnGoXbPFWx7PguT-G1Su_SuZkOwM22ZZHEEE/edit#heading=h.5kzbh922oce3).
Particularly the ability to edit profile information, or to reset or edit the password.
Route | Method | Parameters | Action
---|---|---|---
`user/profile/getCurrentUserProfile/:id` | GET | email | Return all info of the user
`user/editProfile/:id` | POST | email | Update user info according to the arguments (except for the primary email)
`user/updateUserForm/:id` | POST | email | Update user info according to the non-empty arguments
`user/editProfile/updatePrimaryEmail/:id` | POST | user id<br>new email | Send a confirmation link to the new email
`user/resetPassword/checkCurrentPassword/:id` | POST | user id<br>password | Check if the password matches the current one
`user/resetPassword/saveNewPassword/:id` | POST | user id<br>password<br>email (optional) | Save the password to the account with the email or the current logged in user if no email given
`user/updatePrimaryEmail` | POST | jwt token (from the change primary email confirmation link) | Update primary email if the token is valid

## `backend/routes/need.js`

Route | Method | Parameters | Action
---|---|---|---
`need` | POST | Need form | Create a need
`needs` | GET || Fetch all needs
`need/:id` | DELETE || Delete the need with the specified ID
`need/:id` | GET || Fetch the need with the specified ID
`need/:id` | POST | Need form | Update the need with the specified ID using the information in the given form

## `backend/routes/needSatisfier.js`

Route | Method | Parameters | Action
---|---|---|---
`needSatisfier` | POST | Need satisfier form | Create a need satisfier
`needSatisfiers` | GET || Fetch all need satisfiers
`needSatisfier/:id` | DELETE || Delete the need satisfier with the specified ID
`needSatisfier/:id` | GET || Fetch the need satisfier with the specified ID
`needSatisfier/:id` | POST | Need satisfier form | Update the need satisfier with the specified ID using the information in the given form

## `backend/routes/outcome.js`

Route | Method | Parameters | Action
---|---|---|---
`outcome` | POST | Outcome form | Create an outcome
`outcomes` | GET || Fetch all outcomes
`outcome/:id` | DELETE || Delete the outcome with the specified ID
`outcome/:id` | GET || Fetch the outcome with the specified ID
`outcome/:id` | POST | Outcome form | Update the outcome with the specified ID using the information in the given form

  ## `backend/routes/serviceProviders.js`

Route | Method | Parameters | Action
---|---|---|---
`providers` | POST | Provider type<br>Service provider data | Create a service provider
`providers` | GET || Fetch all service providers
`providers/:id` | GET || Fetch the service provider with the specified ID
`providers/:id` | DELETE || Delete the service provider with the specified ID
`provider/:id` | POST | Provider type<br>Service provider data | Update the service provider with the specified ID using the information in the given form
