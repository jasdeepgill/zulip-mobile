# Architecture

## High-level design

**zulip-mobile** uses Redux for state management and data flow. Please
read the [Redux docs](http://redux.js.org) for more information on the Redux
architecture and terminology (such as actions, reducers, and stores).

See [our React/Redux architecture doc](architecture/react.md) for a more
detailed explanation as applied to our app.

At a high-level, global app state should be immutable and should be stored in
a centralized place. Modifying state requires new copies of each data structure.

We use selectors to extract (or select) data from Redux Stores. [Learn more
about the concept of selectors](http://redux.js.org/docs/recipes/ComputingDerivedData.html)
We might use [Reselect](https://github.com/reactjs/reselect) for memoized
selectors, when/if a need for more performance arises.

## Code structure

### Directories

* `/node_modules` - dependencies installed by `yarn` from NPM
* `/android` - auto-generated by React Native
* `/ios` - auto-generated by React Native
* `/docs` - developer documentation
* `/src` - Javascript source code

In general most of the work will be inside of the `/src` directory. The only
reason to touch the `/ios` or `/android` directories would be to add native
modules (which we aren't using at the moment).

### Top-level files
* `package.json` - specifies `yarn` / NPM dependencies and scripts for the project
* `.babelrc` - config file for [Babel](https://babeljs.io/) transpiler (ES6
  -> ES5)
* `.eslintrc` - config file for linting rules (we're using Airbnb rules)
* `.flowconfig` - config file for [Flow](https://flowtype.org/) static type
checker (unused)
* `index.js` - entry point for the app

### `/src` directory

The source directory is broken up into subdirectories corresponding to
components of the app:
* `account` - login, logout, and user account
* `api` - clients for the Zulip server API
* `common` - common components for multiple reuse (buttons, inputs, etc.)
* `compose` - composing messages
* `message` - messages and groups of related messages
* `nav` - navigation
* `streams` - stream of messages
* `users` - user display, search and selection


`ZulipMobile.js` contains the top-level React component for the app and
`boot/reducers.js` contains the top-level reducer.
