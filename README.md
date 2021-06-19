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
guide #0: first steps (removing unecessary parts)
```

#### `step 1: delete src/` - App.js and Index.js only

#### `step 2: delete public/` - favicon.ico and index.html (fix the code) only

#### `step 3: add public/images` - get the images and users from github (store images react - firebase)

#### `step 4: modify src/index.js` - clean it up to basics

#### `step 5: add eslint` - add eslint extension and /.eslintrc.json (npx eslint --init) -> add code from github

```
guide #1: app initialization todos
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
guide #2: second steps (initializing the folder structure)
```

#### `step 1: folder structure src/` - create the todos in folder structure

    - /src
        - components
        - constants
        - context
        - helpers
        - hooks
        - lib
        - services
        - styles

#### `step 2: src/seed.js` - add code from github (run it one time - to avoid duplicate data) (firebase is restricted)

```
the seed file just maps to the representation of our collection and documents.
The seed file simply maps to our collection's and documents' representation.
```

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

    import React from 'react'
    import ReactDOM from 'react-dom'
    import App from './App'
    import FirebaseContext from './context/firebase'
    import {firebase, FieldValue} from './context/firebase'

```
> What is FieldValue? If you do not know, always search to documentation that you aren't familiar with. We are going to use FieldValue 4-5 times when we create our services file -> bunch of functions that allows us to do things.

One of those things, if we want to update the following of a particular account.
Example: User Rafael -> I go ahead follow rafael, if I already followed rafael,     then I can remove from the followers array that we have from the seed.js file.
```

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

```
> get the firebase sdk in the step 8
```

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

```
guide #3: switching to different pages (routers)
```

#### `step 1: yarn add react-router-dom` - pushing users to different pages

    - specify route

#### `step 2: src/App.js` - Bundling,

#### bundle - load the file that the user requests

```
> we can do this in -> webpack, lazy loading (cra), suspense
```

    import { lazy, Suspense } from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';

```
> lazy() - allows us to split huge bundle into chunks.
         - code splitting
            example:
                we only want login page.
                -> const Login = lazy(() => import('./pages/login'));

```

    const Login = lazy(() => import('./pages/login'));


    export default function App() {
    const { user } = useAuthListener();

    return (

        <Router>

```
> <Suspense fallback={} /> - allows us to provide a fallback.
         - show when a Suspense (like React.lazy) child suspends.
         - mao ni mugawas habang naga loading ang imong component.
```

            <Suspense fallback={<p>Loading ... </p>}>
            <Switch>
                <Route path={/login} component={Login} />
            </Switch>
            </Suspense>
        </Router>
    );
    }

#### `step 2: src/pages/login.js` - build login page,

    export default function Login()  {
        return <p>I am the login page </p>
    }

#### `step 3: src/constants/routes.js`

    export const DASHBOARD = '/'
    export const LOGIN = '/login'
    export const SIGN_UP = '/signup'
    export const PROFILE = '/p/:username'
    export const NOT_FOUND = '/not-found'
    //

    /p/karl (:username)
    -> get me :username = karl

    /p/steve (:username)
    -> get me :username = steve

#### `step 4: src/App.js`

    import { lazy, Suspense } from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import * as ROUTES from './constants/routes'

```
>In computer programming, a constant is a value that should not be altered by the program during normal execution
```

    const Login = lazy(() => import('./pages/login'));


    export default function App() {
    const { user } = useAuthListener();

    return (

        <Router>
            <Suspense fallback={<p>Loading ... </p>}>
            <Switch>
                <Route path={ROUTES.LOGIN} component={Login} />
            </Switch>
            </Suspense>
        </Router>
    );
    }

#### `step 4: src/pages/login.js`

    import {useState,useContext,useEffect} from 'react'

```
>why context? we need it when user signin, logs-in, check if the user already exist.
```

```
>why state? it allows us to store value in there.
```

    import {useHistory} from "react-router-dom"

```
>useHistory allows us to navigate user elsewhere.
User Logs-in -> navigate to dashboard.
```

    import FirebaseContext from '../context/firebase'



    export default function Login() {
        const history = useHistory()
        const { firebase } = useContext(FirebaseContext)

        const [emailAdress, setEmailAddress] = useState('')
        const [password, setPassword] = useState('')

        const [error, setError] = useState('')
        const isInvalid = password === '' || emailAddress === ''

        const handleLogin = () => {}

        useEffect(() => {
            document.title = 'Login - Instagram'
        }, [])

```
>how useEffect works? it runs on first initial render, if you put something in (dependency array) [] for example [password] it will run eachtime password changes.
If we happen to delete (dependency array) [] it will just keep rerendering, each time rerenders calls it will call the useEffect function.
```

        return
        (
        <div className="container flex mx-auto max-w-screen-md items-center h-screen">
            <p>I am the login page</p>
        </div>
        )
    }

```
guide #3: setting up and using (tailwindcss)
```

    -> yarn add tailwindcss -D

```
>tailwindcss is like bootstrap but thousand times better, it allows us to use utilities (classnames). We can define our own signature of the classname.
```

    -> yarn add prop-types -D

```
The 'prop-types' library is used to type check data as it moves into a component. PropTypes can help us debug our code more efficiently and ensure that our code is squeaky clean before deployment.
```

    -> yarn add postcss-cli -D
    -> yarn add postcss -D

```
Transform styles with JS plugins. It helps us run our css to different browsers (ie, firefox, chrome, etc.) so to not put the syntax for all, I want to target IE 8,9,10. It works pretty well!
```

    -> yarn add npm-run-all -D

```
A CLI tool to run multiple npm-scripts in parallel or sequential.
```

    -> yarn add autoprefixer -D

#### `step 1: package.json`

    "scripts" : {
        "build:css": "postcss src/styles/tailwind.css -o src/styles/app.css",
        "watch:css": "postcss src/styles/tailwind.css -o src/styles/app.css --watch",

```
Why watch? if we change the file, we want it to reload and also regenerate the file.
```

        "react-scripts:start": "sleep 5 && react-scripts start",
        "dist": "react-scripts build",

```
Why dist? if we want to distribute our app, create dist, so to put this on the website.

```

        "start": "run-p watch:css react-scripts:start",

```
start: modify it so that we can also run tailwind along with the scripts.
```

        "build": "run-s build:css react-scripts:build",

    }

#### `step 2: src/styles/tailwind.css`

    @tailwind base;
    @tailwind components;
    @tailwind utilities;

#### `step 3: cmd` -> yarn start

#### `step 4: src/index.js`

    import React from 'react'
    import ReactDOM from 'react-dom'
    import App from './App'
    import FirebaseContext from './context/firebase'
    import {firebase, FieldValue} from './context/firebase'
    import './styles/app.css'

    ReactDOM.render (
        <FirebaseContext.Provider value={{ firebase, FieldValue}}>
            <App />
        </FirebaseContext.Provider>
        document.getElementById('root')
    )

#### `step 4: /postcss.config.js`

    module.exports = {
        plugins: [require('tailwindcss'), require('autoprefixer')]
    };

#### `step 5: /tailwind.config.js` -> without this tailwind will not let your app to run, lol.

    module.exports = {
        future: {
            removeDeprecatedGapUtilities: true

```
> This let's us be on the future version updates whereas for us being depricated, so we are up for that particular version.
```

        }
    }

#### `step 4: src/pages/login.js` - setting up tailwind css and

    import {useState,useContext,useEffect} from 'react'
    import {Link, useHistory} from "react-router-dom"
    import FirebaseContext from '../context/firebase'



    export default function Login() {
        const history = useHistory()
        const { firebase } = useContext(FirebaseContext)

        const [emailAdress, setEmailAddress] = useState('')
        const [password, setPassword] = useState('')

        const [error, setError] = useState('')
        const isInvalid = password === '' || emailAddress === ''

        const handleLogin = () => {}

```
> This let's us contact and communicate with firebase, by using this we are not going to have a problem on creating database, handling an authentication, it's a pain.
```

        useEffect(() => {
            document.title = 'Login - Instagram'
        }, [])

        return
        (
        <div className="container flex mx-auto max-w-screen-md items-center h-screen">
            <div className="flex w-3/5">
                <img src="/images/iphone-with-profile.jpg" alt="iPhone with Instagram app" className="max-w-full"/>
            </div>

            <div className="flex flex-col w-2/5">
                <p> I will be the form! </p>
            </div>
        </div>
        )
    }

##### we need form, error handling, logo

#### `step 4: src/pages/login.js` - logo, email & password and login & signup btn

```
> focus on the form at this moment, we are going to have things like:
```

    - email
    - password
    - add some validation
    - opacity (if validation is incorrect, we want button to be 50% opacity)



        return
        (

        <div className="container flex mx-auto max-w-screen-md items-center h-screen">
            <div className="flex w-3/5">
                <img src="/images/iphone-with-profile.jpg" alt="iPhone with Instagram app" className="max-w-full"/>
            </div>

            <div className="flex flex-col w-2/5">
                <div className="flex flex-col items-center bg-white p-4 border border-gray-primary mb-4 rounded">
                <h1 className="flex justify-center w-full">
                    <img src="/images/logo.png" alt="Instagram" className="mt-2 w-6/12 mb-4" />
                </h1>
                {error && <p className="mb-4 text-xs text-red-primary">{error}</p>}

                <form onSubmit={handleLogin} method="POST">
                    <input
                        aria-label="Enter your email address"
                        type="text"
                        placeholder="Email address"
                        className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border border-gray-primary rounded mb-2"
                        onChange={({ target }) => setEmailAddress(target.value)}
                        value={emailAddress}
                    />
                    <input
                        aria-label="Enter your password"
                        type="password"
                        placeholder="Password"
                        className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border border-gray-primary rounded mb-2"
                        onChange={({ target }) => setPassword(target.value)}
                        value={password}
                    />

```
> semantically, you want input elements to be inside of forms.
- TODO: add to tailwind config
    - bg-blue-medium -> hex values
    - text-red-primary -> hex values
    - text-blue-medium -> hex values
    - text-gray-base -> hex values
    - border-gray-primary -> hex values
```

                    <button
                        disabled={isInvalid}
                        type="submit"
                        className={`bg-blue-medium text-white w-full rounded h-8 font-bold
                        ${isInvalid && 'opacity-50'}`}
                        >
                        Login
                    </button>
                </form>
            </div>
            <div className="flex justify-center items-center flex-col w-full bg-white p-4 rounded border border-gray-primary">
                <p className="text-sm">
                    Don't have an account?{` `}
                    <Link to={ROUTES.SIGN_UP} className="font-bold text-blue-medium">
                    Sign up
                    </Link>
                </p>
            </div>
            </div>
        </div>
        )

#### `step 5: /tailwind.config.js` - setup tailwindcss customization

```
- TODO: add to tailwind config
    - bg-blue-medium -> hex values
    - text-red-primary -> hex values
    - text-blue-medium -> hex values
    - text-gray-base -> hex values
    - border-gray-primary -> hex values
```

        module.exports = {
            future: {
                removeDeprecatedGapUtilities: true
            },
            theme: {
                fill: (theme) => ({
                red: theme('colors.red.primary')
                }),
                colors: {
                    white: '#ffffff',
                    blue: {
                        medium: '#005c98'
                    },
                    black: {
                        light: '#262626',
                        faded: '#00000059'
                    },
                    gray: {
                        base: '#616161',
                        background: '#fafafa',
                        primary: '#dbdbdb'
                    },
                    red: {
                        primary: '#ed4956'
                    }
                }
            }
        };

#### `step 6: src/pages/login.js` - focusing on the error

    import {useState,useContext,useEffect} from 'react'
    import {Link, useHistory} from "react-router-dom"
    import FirebaseContext from '../context/firebase'
    import * as ROUTES from '../constants/routes'


    export default function Login() {
        const history = useHistory()
        const { firebase } = useContext(FirebaseContext)

        const [emailAdress, setEmailAddress] = useState('')
        const [password, setPassword] = useState('')

        const [error, setError] = useState('')
        const isInvalid = password === '' || emailAddress === ''

        const handleLogin = async (event) => {
            event.preventDefault()

            try {
                await firebase.auth().signInWithEmailAndPassword(emailAddress, password);
                history.push(ROUTES.DASHBOARD);

```
> There would be the case that we will recieve an error, what to do are the following.
```

            } catch (error) {
                setEmailAddress('');
                setPassword('');
                setError(error.message);
            }
        }

```
> This let's us contact and communicate with firebase, by using this we are not going to have a problem on creating database, handling an authentication, it's a pain.
```

        useEffect(() => {
            document.title = 'Login - Instagram'
        }, [])

#### `step 6: src/App.js` - add signup route

    import { lazy, Suspense } from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import * as ROUTES from './constants/routes'

    const Login = lazy(() => import('./pages/login'));
    const Signup = lazy(() => import('./pages/signup'));


    export default function App() {
    const { user } = useAuthListener();

    return (

        <Router>
            <Suspense fallback={<p>Loading ... </p>}>
                <Switch>
                    <Route path={ROUTES.LOGIN} component={Login} />
                    <Route path={ROUTES.SIGN_UP} component={SignUp} />
                </Switch>
            </Suspense>
        </Router>
    );
    }

#### `step 9: src/services/firebase.js` - building signup page

    import { firebase, FieldValue } from '../lib/firebase';

    export async function doesUsernameExist(username) {
        const result = await firebase
        .firestore()
        .collection('users')
        .where('username', '==', username)
        .get();

        return result.docs.length > 0;
    }

#### `step 8: src/pages/signup.js` - building signup page

    import { useState, useContext, useEffect } from 'react';
    import { Link, useHistory } from 'react-router-dom';
    import FirebaseContext from '../context/firebase';
    import * as ROUTES from '../constants/routes';
    import { doesUsernameExist } from '../services/firebase';

    export default function SignUp() {
      const history = useHistory();
      const { firebase } = useContext(FirebaseContext);

      const [username, setUsername] = useState('');
      const [fullName, setFullName] = useState('');
      const [emailAddress, setEmailAddress] = useState('');
      const [password, setPassword] = useState('');

      const [error, setError] = useState('');
      const isInvalid = password === '' || emailAddress === '';

      const handleSignUp = async (event) => {
        event.preventDefault();

        const usernameExists = await doesUsernameExist(username);
        if (!usernameExists) {
          try {
            // create the user with email and password
            const createdUserResult = await firebase
              .auth()
              .createUserWithEmailAndPassword(emailAddress, password);

```
> The reasoning behind assigning the above firebase request to createdUserResult variable is because "I want to link it on a certain details, the email and password is going to authentication for firebase as well as the email is going over to firestore"
```

            // authentication
                // -> emailAddress & password & username (displayName)
            await createdUserResult.user.updateProfile({
              displayName: username
            });

            // firebase user collection (create a document)
            await firebase
              .firestore()
              .collection('users')
              .add({
                userId: createdUserResult.user.uid,
                username: username.toLowerCase(),
                fullName,
                emailAddress: emailAddress.toLowerCase(),
                following: ['2'],
                followers: [],
                dateCreated: Date.now()
              });

            history.push(ROUTES.DASHBOARD);
          } catch (error) {
                setFullName('');
                setEmailAddress('');
                setPassword('');
                setError(error.message);
          }
        } else {
          setUsername('');
          setError('That username is already taken, please try another.');
        }
      };

      useEffect(() => {
        document.title = 'Sign Up - Instagram';
      }, []);

      return (
        <div className="container flex mx-auto max-w-screen-md items-center h-screen">
          <div className="flex w-3/5">
            <img src="/images/iphone-with-profile.jpg" alt="iPhone with Instagram app" /    >
          </div>
          <div className="flex flex-col w-2/5">
            <div className="flex flex-col items-center bg-white p-4 border  border-gray-primary mb-4 rounded">
              <h1 className="flex justify-center w-full">
                <img src="/images/logo.png" alt="Instagram" className="mt-2 w-6/12  mb-4" />
              </h1>

              {error && <p className="mb-4 text-xs text-red-primary">{error}</p>}

              <form onSubmit={handleSignUp} method="POST">
                <input
                  aria-label="Enter your username"
                  type="text"
                  placeholder="Username"
                  className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border    border-gray-primary rounded mb-2"
                  onChange={({ target }) => setUsername(target.value)}
                  value={username}
                />
                <input
                  aria-label="Enter your full name"
                  type="text"
                  placeholder="Full name"
                  className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border    border-gray-primary rounded mb-2"
                  onChange={({ target }) => setFullName(target.value)}
                  value={fullName}
                />
                <input
                  aria-label="Enter your email address"
                  type="text"
                  placeholder="Email address"
                  className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border    border-gray-primary rounded mb-2"
                  onChange={({ target }) => setEmailAddress(target.value)}
                  value={emailAddress}
                />
                <input
                  aria-label="Enter your password"
                  type="password"
                  placeholder="Password"
                  className="text-sm text-gray-base w-full mr-3 py-5 px-4 h-2 border    border-gray-primary rounded mb-2"
                  onChange={({ target }) => setPassword(target.value)}
                  value={password}
                />
                <button
                  disabled={isInvalid}
                  type="submit"
                  className={`bg-blue-medium text-white w-full rounded h-8 font-bold
                ${isInvalid && 'opacity-50'}`}
                >
                  Sign Up
                </button>
              </form>
            </div>
            <div className="flex justify-center items-center flex-col w-full bg-white   p-4 rounded border border-gray-primary">
              <p className="text-sm">
                Have an account?{` `}
                <Link to={ROUTES.LOGIN} className="font-bold text-blue-medium">
                  Login
                </Link>
              </p>
            </div>
          </div>
        </div>
      );
    }

```
> useRef() - You can have ref if you worried about how much data is being updated each time when someone types, that's fine.
> Javascript falsy values
```

#### `step 9: src/App.js` - add notfound route

    import { lazy, Suspense } from 'react';
    import { BrowserRouter as Router, Route, Switch } from 'react-router-dom';
    import * as ROUTES from './constants/routes'

    const Login = lazy(() => import('./pages/login'));
    const Signup = lazy(() => import('./pages/signup'));
    const NotFound = lazy(() => import('./pages/notfound'));


    export default function App() {
    const { user } = useAuthListener();

    return (

        <Router>
            <Suspense fallback={<p>Loading ... </p>}>
                <Switch>
                    <Route path={ROUTES.LOGIN} component={Login} />
                    <Route path={ROUTES.SIGN_UP} component={SignUp} />
                    <Route component={NotFound} />
                </Switch>
            </Suspense>
        </Router>
    );
    }

#### `step 9: src/pages/notfound.js` - building signup page

    import { useEffect } from 'react';

    export default function NotFound() {
        useEffect(() => {
            document.title = 'Not Found - Instagram';
        }, []);
        return (
            <div className="bg-gray-background">
                <div className="mx-auto max-w-screen-lg">
                    <p className="text-center text-2xl">Not Found!</p>
                </div>
            </div>
        )
    }

#### `step 10: src/pages/dashboard.js` - building dashboard page

    import { useEffect } from 'react';
    import PropTypes from 'prop-types';
    import Header from '../components/header';
    import Timeline from '../components/timeline';
    import Sidebar from '../components/sidebar';
    import useUser from '../hooks/use-user';
    import LoggedInUserContext from '../context/logged-in-user';

    export default function Dashboard({ user: loggedInUser }) {
      const { user, setActiveUser } = useUser(loggedInUser.uid);
      useEffect(() => {
        document.title = 'Instagram';
      }, []);

      return (
        <LoggedInUserContext.Provider value={{ user, setActiveUser }}>
          <div className="bg-gray-background">
            <Header />
            <div className="grid grid-cols-3 gap-4 justify-between mx-auto  max-w-screen-lg">
              <Timeline />
              <Sidebar />
            </div>
          </div>
        </LoggedInUserContext.Provider>
      );
    }

    Dashboard.propTypes = {
      user: PropTypes.object.isRequired
    };

#### `step 11: src/components/timeline.js` - building timeline component

    import { useContext } from 'react';
    import Skeleton from 'react-loading-skeleton';
    import LoggedInUserContext from '../context/logged-in-user';
    import usePhotos from '../hooks/use-photos';
    import Post from './post';

    export default function Timeline() {
        const { user } = useContext(LoggedInUserContext);
        const { photos } = usePhotos(user);

        return (
        <div className="container col-span-2">
            {!photos ? (
            <Skeleton count={4} width={640} height={500} className="mb-5" />
            ) : (
            photos.map((content) => <Post key={content.docId} content={content} />)
            )}
        </div>
        );
    }

#### `step 12: src/components/sidebar.js` - building sidebar component

#### `step 13: src/components/header.js` - building header component

#### `step 14: src/App.js` - Fix routing put Dashboard

#### `step 15: src/components/header.js` - building header component

- todos
  - access to firebase
  - context to user

#### `step 16: src/hooks/use-auth-listener.js` - listen if the user logs in or logs out

- todos
  - useState for user
  - useEffect to listen for changes
  - useContext to listen to firebase
  - onAuthStateChanged in firebase there is this to also listen to firebase
  - put firebase on useEffect dependency array and clean up listener
  - using the hook:
    - 1.) use this hook potentially to the top level of the application, so that the routes have access on the hook. (top to bottom)
    - 2.) use this hook as context instead of top level

#### `step 18: src/context/user.js` - create user context to connect to the use-auth-listener (that is listening for the state to change), so that to avoid recalling the use-auth-listener again and again.

- todos
  - copy firebase context and replace it to user

#### `step 19: src/hooks/App.js` - use the useAuthListener()

- todos
  - create usercontext provider to let the consumer child components access it.

#### `step 20: src/components/header.js` - pull out usercontext

- todos

  - import FirebaseContext
  - import UserContext
  - import ROUTES
  - import Link
  - firebase and user -> useContext
  - check application if the user info is in there

    <header className="h-16 bg-white border-b border-gray-primary mb-8">
          <div className="container mx-auto max-w-screen-lg h-full">
            <div className="flex justify-between h-full">
              <div className="text-gray-700 text-center flex items-center align-items cursor-pointer">
                <h1 className="flex justify-center w-full">
                  <Link to={ROUTES.DASHBOARD} aria-label="Instagram logo">
                    <img src="/images/logo.png" alt="Instagram" className="mt-2 w-6/12" />
                  </Link>
                </h1>
              </div>
              <div className="text-gray-700 text-center flex items-center align-items">
                {loggedInUser ? (
                  <>
                    <Link to={ROUTES.DASHBOARD} aria-label="Dashboard">
                      <svg
                        className="w-8 mr-6 text-black-light cursor-pointer"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          strokeLinecap="round"
                          strokeLinejoin="round"
                          strokeWidth={2}
                          d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"
                        />
                      </svg>
                    </Link>

                    <button
                      type="button"
                      title="Sign Out"
                      onClick={() => {
                        firebase.auth().signOut();
                        history.push(ROUTES.LOGIN);
                      }}
                      onKeyDown={(event) => {
                        if (event.key === 'Enter') {
                          firebase.auth().signOut();
                          history.push(ROUTES.LOGIN);
                        }
                      }}
                    >
                      <svg
                        className="w-8 mr-6 text-black-light cursor-pointer"
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke="currentColor"
                      >
                        <path
                          strokeLinecap="round"
                          strokeLinejoin="round"
                          strokeWidth={2}
                          d="M17 16l4-4m0 0l-4-4m4 4H7m6 4v1a3 3 0 01-3 3H6a3 3 0 01-3-3V7a3 3 0 013-3h4a3 3 0 013 3v1"
                        />
                      </svg>
                    </button>
                    {user && (
                      <div className="flex items-center cursor-pointer">
                        <Link to={`/p/${user?.username}`}>
                          <img
                            className="rounded-full h-8 w-8 flex"
                            src={`/images/avatars/${user?.username}.jpg`}
                            alt={`${user?.username} profile`}
                            onError={(e) => {
                              e.target.src = DEFAULT_IMAGE_PATH;
                            }}
                          />
                        </Link>
                      </div>
                    )}
                  </>
                ) : (
                  <>
                    <Link to={ROUTES.LOGIN}>
                      <button
                        type="button"
                        className="bg-blue-medium font-bold text-sm rounded text-white w-20 h-8"
                      >
                        Log In
                      </button>
                    </Link>
                    <Link to={ROUTES.SIGN_UP}>
                      <button
                        type="button"
                        className="font-bold text-sm rounded text-blue-medium w-20 h-8"
                      >
                        Sign Up
                      </button>
                    </Link>
                  </>
                )}
              </div>
            </div>
          </div>
        </header>
