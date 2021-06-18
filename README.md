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
    import {useHistory} from "react-router-dom"
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

#### `step 4: src/pages/login.js` - logo, email and password

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
        </div>
        )
