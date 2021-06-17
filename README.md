# Getting Started with Create React App

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `yarn start`

Runs the app in the development mode.\
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.\
You will also see any lint errors in the console.

### `yarn test`

Launches the test runner in the interactive watch mode.\
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.\
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.\
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

### Code Splitting

This section has moved here: [https://facebook.github.io/create-react-app/docs/code-splitting](https://facebook.github.io/create-react-app/docs/code-splitting)

### Analyzing the Bundle Size

This section has moved here: [https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size](https://facebook.github.io/create-react-app/docs/analyzing-the-bundle-size)

### Making a Progressive Web App

This section has moved here: [https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app](https://facebook.github.io/create-react-app/docs/making-a-progressive-web-app)

### Advanced Configuration

This section has moved here: [https://facebook.github.io/create-react-app/docs/advanced-configuration](https://facebook.github.io/create-react-app/docs/advanced-configuration)

### Deployment

This section has moved here: [https://facebook.github.io/create-react-app/docs/deployment](https://facebook.github.io/create-react-app/docs/deployment)

### `yarn build` fails to minify

This section has moved here: [https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify](https://facebook.github.io/create-react-app/docs/troubleshooting#npm-run-build-fails-to-minify)

## Dependencies

### `yarn add date-fns` 1 - let's us add dates easily

### `yarn add firebase` 2 - backend connection

### `yarn add react-loading-skeleton` 3 -skeleton UI

## Creating reactjs instagram with firebase

### first steps (removing unecessary parts)

#### `step 1: delete src/` - App.js and Index.js only

#### `step 2: delete public/` - favicon.ico and index.html (fix the code) only

#### `step 3: add public/images` - get the images and users from github (store images react - firebase)

#### `step 4: modify src/index.js` - clean it up to basics

#### `step 5: add eslint` - add eslint extension and /.eslintrc.json (npx eslint --init) -> add code from github

### guide #1: app initialization todos

- client side rendered app: react(cra)
  - database which is Firebase
  - react-loading-skeleton
  - tailwind
- folder structure
  - /src
    - components
    - constants
    - context
    - helpers
    - hooks
    - pages
    - lib (firebase is going to live in here)
    - services (firebase functions in here)
    - styles (tailwind's folder (app/tailwind))

### second steps (initializing the folder structure)

#### `step 1: folder structure src/` - create the todos in folder structure

    - /src
        - components
        - constants
        - context
        - helpers
        - hooks
        - lib
        -services

#### `step 2: src/seed.js` - add code from github (run it one time - to avoid duplicate data) (firebase is restricted)

#### `step 3: setup/firebase` - get the images and users only (store images react - firebase)
