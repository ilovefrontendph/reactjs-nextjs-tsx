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

### `yarn add react-router-dom` 4 - pushing users to different pages

## Creating reactjs instagram with firebase

```
### guide #0: first steps (removing unecessary parts)
```

#### `step 1: delete src/` - App.js and Index.js only

#### `step 2: delete public/` - favicon.ico and index.html (fix the code) only

#### `step 3: add public/images` - get the images and users from github (store images react - firebase)

#### `step 4: modify src/index.js` - clean it up to basics

#### `step 5: add eslint` - add eslint extension and /.eslintrc.json (npx eslint --init) -> add code from github

```
### guide #1: app initialization todos
```

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

```
### guide #2: second steps (initializing the folder structure)
```

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

#### `step 3: setting up firebase` - go to firebase.google.com

    - console
        - add project
            - step 1: app name (instagram)
            - step 2: disable google analytics
    - cloud firestore
        - create database
            -start in test mode (allows read and write)
                - Philippines (asia-northeast2) -> switch to southeast
                - Enable
    - rules
        - copy code from /firebase-rules.png
    - data (house full of collection)
        - collection (photos)
            - autoid (delete document)
        - collection (users)
            - autoid (delete document)
    - authentication
        - Sign-in method
            - enable (Email/Password)
        - Users
            - mckeenasma123@gmail.com
            - test123
            - note get the user ID and paste it in src/seed.js

#### `step 4: /src/seed.js` - change the userID

#### `step 5: /src/context/firebase.js` - connection to the firestore

    import createContext from 'react'
    const FirebaseContext = createContext(null)
    export default FirebaseContext
        - context allows us to insert information

            // This is how context works
            // provider and consumer (if you want the component to access firebase)
            provider------ component 1 ------ (firebase init here)
            ------ component 2 ------
            ------ component 3 ------
            consumer------ component 4 ------ (firebase init here)
            ------ component 5 ------
            ------ component 6 ------
            ------ component 7 ------
            ------ component 8 ------
            consumer------ component 9 ------ (firebase init here)

#### `step 6: /src/index.js` - use FirebaseContext

    import FirebaseContext from './context/firebase'
    import {firebase, FieldValue} from './context/firebase'

    ReactDOM.render (
        <FirebaseContext.Provider value={{ firebase, FieldValue}}>
            <App />
        </FirebaseContext.Provider>
        document.getElementById('root')
    )

#### `step 7: /src/lib/firebase.js` - initialize application, seed firebase

    import Firebase from 'firebase/app';
    import 'firebase/firestore';
    import 'firebase/auth';

    // here I want to import the seed file
    // import { seedDatabase } from '../seed'

    const config = {
    apiKey: '',
    authDomain: '',
    projectId: '',
    storageBucket: '',
    messagingSenderId: '',
    appId: ''
    };
    // firebase sdk

    const firebase = Firebase.initializeApp(config);
    const { FieldValue } = Firebase.firestore;

    // here is where I want to call the seed file (only Once!)
    // seedDatabase(firebase)

    export { firebase, FieldValue };

#### `step 8: firebase/firestore` - initialize application

        - general
            - web
                - (web name) instagram yt
                - register app
                - copy firebase sdk

### `guide #3: switching to different pages (routers)`

#### `step 1: yarn add react-router-dom` - pushing users to different pages

    - specify route

#### `step 2: src/App.js` - Bundling,

#### bundle - load the file that the user requests

```
> we can do this in -> webpack, lazy loading (cra), suspense
```

    import { lazy, Suspense } from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import ReactLoader from './components/loader';
    import * as ROUTES from './constants/routes';
    import UserContext from './context/user';
    import useAuthListener from './hooks/use-auth-listener';

    import ProtectedRoute from './helpers/protected-route';

```
> lazy() - allows us to split huge bundle into chunks.
         - code splitting
            example:
                we only want login page.
                -> const Login = lazy(() => import('./pages/login'));

```

    const Login = lazy(() => import('./pages/login'));
    const SignUp = lazy(() => import('./pages/sign-up'));
    const Dashboard = lazy(() => import('./pages/dashboard'));
    const Profile = lazy(() => import('./pages/profile'));
    const NotFound = lazy(() => import('./pages/not-found'));


    export default function App() {
    const { user } = useAuthListener();

    return (
        <UserContext.Provider value={{ user }}>
        <Router>

```
> lazy() - allows us to provide a fallback.
         - show when a Suspence (like React.lazy) child suspends.
            example:
                we only want login page.
                -> const Login = lazy(() => import('./pages/login'));

```

            <Suspense fallback={<ReactLoader />}>
            <Switch>
                <Route path={ROUTES.LOGIN} component={Login} />
                <Route path={ROUTES.SIGN_UP} component={SignUp} />
                <Route path={ROUTES.PROFILE} component={Profile} />
                <ProtectedRoute user={user} path={ROUTES.DASHBOARD} exact>
                <Dashboard />
                </ProtectedRoute>
                <Route component={NotFound} />
            </Switch>
            </Suspense>
        </Router>
        </UserContext.Provider>
    );
    }

#### `step 2: src/pages/login.js` - build login page,

    export default function Login()  {
        return <p>I am the login page </p>
    }
