# Truecaller Blog Frontend

## Description

This project is a simple frontend for the Truecaller Blog using Vue.js. It displays a list of blog posts and allows filtering by category. Clicking on a post shows the post details.

## Setup

1. Clone the repository.
2. Navigate to the project directory.
3. Install dependencies with `npm install`.
4. Run the project with `npm run serve`.

## Project Structure

- `public/`: Contains the `index.html` file.
- `src/`: Contains the source code for the application.
  - `assets/`: Contains static assets such as images.
  - `components/`: Contains Vue components.
  - `views/`: Contains view components.
  - `router/`: Contains the router configuration.
  - `App.vue`: The root component.
  - `main.js`: The entry point for the application.

## Components

- `PostCard.vue`: Displays a summary of a post.
- `PostList.vue`: Displays a list of posts with filtering and pagination.
- `PostDetail.vue`: Displays the details of a single post.

## Views

- `HomeView.vue`: Displays the home page with the list of posts.
- `PostView.vue`: Displays the details of a single post.

## API

- `https://public-api.wordpress.com/rest/v1.1/sites/107403796/posts/`: Fetches the list of posts.
- `https://public-api.wordpress.com/rest/v1.1/sites/107403796/categories`: Fetches the list of categories.
- `https://public-api.wordpress.com/rest/v1.1/sites/107403796/posts/slug:${SLUG}`: Fetches the details of a single post.

## Notes

- The project uses Vue Router for navigation.
- Axios is used for making API requests.
- The date is formatted to show how long ago the post was published.

## Assumptions

- The project is kept simple and does not include complex UI elements.
- No unit tests are included in this submission.

## Future Improvements

- Add unit tests.
- Improve the UI/UX with more styling and animations.
- Implement caching for API requests.
