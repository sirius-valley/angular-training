# Sirius Twitter - Angular Training

Welcome to the Sirius Twitter - Angular Training! This project is designed to help you learn Angular.

## Index
1. [The Project](#the-project)
2. [Design](#design)
3. [Features](#features)
4. [Mandatory Considerations](#mandatory-considerations)
5. [Optional Considerations](#optional-considerations)

## The project

The project consists of building a Twitter clone using Angular and integrating it with a previously implemented [backend application](https://server-para-fecundi.onrender.com/).

The backend application is an API similar to Twitter and includes features like user follow/unfollow, private profiles, cursor-based pagination, post reactions, comments, user profile pictures, real-time chat, and more. 

The backend endpoints will be utilized wherever necessary to communicate with the backend API and implement the various features of the Twitter clone. The project will result in a complete Twitter clone that utilizes the latest frontend technologies and follows best practices for performance, maintainability, and scalability.

[Swagger Docs for API](https://server-para-fecundi.onrender.com/docs/#/)

## Design
The web app should follow the design system and screens from the well-crafted [FIGMA](https://www.figma.com/file/BHEwOsKUxQjLMNydqkNkcz/Twitter-App?type=design&node-id=1%3A3&mode=design&t=hUo8AS3ofmPqyJS3-1) made by the Sirius Software Design Team.

[Figma for Design](https://www.figma.com/file/BHEwOsKUxQjLMNydqkNkcz/Twitter-App?type=design&node-id=1%3A3&mode=design&t=hUo8AS3ofmPqyJS3-1)

## Features

### 1. Register: Create a register screen. 
User should provide the following information:
  - ***Name***: String.
  - ***Email***: String.
  - ***Username***: String.
  - ***Password***: String.

    Use `POST api/auth/signup`

#### Additional Considerations
- Server and validation errors should be handled and displayed to the user.

- All fields should be validated. Name and Username can't be empty. Email must match the email format and password should be strong (One uppercase, one number, one special symbol and eight (8) or more characters).

- Once the user successfully registers, it should save the access token (JWT) for sending requests.

### 2. Login: Create a login screen, that works as entry point to the application. 
User should provide the following information:
  - ***Username***: String.
  - ***Password***: String.

Use `POST api/auth/login`

#### Additional Considerations
- Server and validation errors should be handled and displayed to the user.

- Once the user successfully signs in, it should save the access token (JWT)  for sending requests.

### 3. Tweet: After logging in, user should be able to post.
Posts should contain:
  - ***Content***: String with 1 to 240 characters.
  - ***Images***: Array with 0-4 image URLs. (Optional). Let user upload images to S3 and use generated links.

  Use `POST api/post`.

#### Additional Considerations
- After posting, user should see their post without having to refresh the page (This can be done in the **Feed** task).


### 4. Feed: Create a posts feed, which should work as the "Home" screen. 
Here, the logged users should see posts from themselves and from followed users. Posts should show:
  - ***Content***
  - ***Images***: If existent.

  Profile screen should use the same UI component as the feed.
  Use `GET api/post`.

#### Additional Considerations
- Tweets must be displayed with an infinite scroll. Once the user scrolls down, new tweets should be fetched.

### 5. React to post: Add reactions (like and repost) to posts, both in profile screens and feed. 

Use `POST api/reaction/:post_id` to add a reaction (like) and `DELETE api/reaction/:post_id` to delete it.

#### Additional Considerations

### 6. Comment post: Add a button to comment a post. 
The comment should have:
  - ***Content***: String with 1 to 240 characters.
  - ***Images***: Array with 0-4 image URLs. (Optional). Let user upload images to S3 and use generated links.
  
  Reuse post component to create a new comment.
  Use the endpoint created in the backend.

### Display comments and reactions in posts: Display the number of comments, likes and reposts for each post.

Also, display a list of comments under each post (after clicking on it), with infinite scroll.

### 7. User recommendations: Add a list of users recommended on the right side of the feed. 
Show only first 4 recommended users, with:
  - ***Name***
  - ***Username***
  - ***Profile picture***: Default to avatar with initials.
  - ***Follow button***: After clicking on follow, user should disappear from the list, and the next recommended user should appear.

  Use `GET api/user`.

#### Additional Considerations
- Under the last user, there should be a "See more" button, which redirects the user to a screen with recommended users, with infinite scroll.

### 8. Delete post: User should be able to delete their own posts. 
Use `DELETE api/post/:post_id`.

#### Additional Considerations
- Before deleting the post, a confirmation modal should be displayed.

### 9. Profile: After clicking on profile image, user should navigate to their profile. 
Here, they should see:
  - ***Name***
  - ***Username***
  - ***Posts***

  Use `GET api/user/me` and `GET api/post/by_user/:user_id`.

#### Additional Considerations
- If user has no image, it should default to avatar with initials.

### 10. Delete user: Add a button "Delete" that lets users delete their accounts. 
After deleting the account, user should be redirected to the login screen. 
Use `DELETE api/user`.

#### Additional Considerations
- Before deleting the user, a confirmation modal should be displayed with the corresponding warnings. 

### 11. Search user: Add a search bar that lets user search other users by username, and displays options with:
  - ***Name***
  - ***Username***
  - ***Profile image***: Default to avatar with initials.

  Use `GET api/user/:userId`. Users list should have infinite scroll.

### 12. User profile: After finding and clicking on a user, user should be redirected to the other users profile screen. 
This screen should display:
  - ***Name***
  - ***Username***
  - ***Posts***: Only if profile is public or current user follows this user. If not, show a message "User has a private account".

Use `GET api/user/:user_id`.

#### Additional Considerations
- Reuse own profile's screen

### 13. Follow user: Add a "Follow" button to other users profile screen. 
Use `POST /api/follower/follow/:user_id`. Should only display if user isn't currently following the other user.

### 14. Unfollow user: Add an "Unfollow" button to other users profile screen. 
Use ```POST /api/follow/unfollow/:user_id```. Should only display if user is currently following the other user.

#### Additional Considerations
- After unfollowing, posts should hide if other user's account is private, without having to refresh.

## Mandatory considerations
- Routes should be protected. All screens should contain some access validation (except for login and register).
- Components and services must be tested.
- Reuse common components
- The application should adjust to Figma designs
- The application should be responsive:
  - Mobile: 360×640 - 414×896
  - Tablet: 601×962 - 1280×800
  - Desktop: 1024×768 - 1920×1080
- The app should handle errors:
  - If error doesn't block the application's lifecycle, then show screen's error state (if designed) or a toast (if not designed).
  - If error blocks the user from using the application, redirect to a default screen with an option to report the error with some kind of error handling or boundary.
- Use environment variables to hide keys and application environment (development/production).

## Optional Considerations

- Include i18n spanish and english translations
- Include dark/light mode option

Happy coding! 👨‍💻
