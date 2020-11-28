# Organized for Deployment

A model of how you can set up your project for development, testing & deployment.

### Contents

* [Directory Structure](#directory-structure)
* [Development](#development)
  * [API](#api)
  * [Client](#client)
  * [Full App](#full-app)
* [Deployment](#deployment)
  * [Mock](#mock)
  * [Manual](#manual)
  * [Automated](#automated)
* [Testing](#testing)
  * [Frontend](#Frontend)
  * [Backend](#backend)
* [Helpful Links](#helpful-links)

---

## Directory Structure


```
.
├── .circleci/
|   └── config.yml
|
├── api/
|   ├── db
|   │   └── README.md
|   ├── dev.js
|   ├── middleware.js
|   ├── models
|   │   └── User.js
|   ├── routes
|   │   ├── home.js
|   │   ├── login.js
|   │   └── test.js
|   ├── server.js
|   └── __test__
|       └── example.spec.js`
|
├── client/
│   ├── build
│   ├── coverage
│   ├── package.json
│   ├── package-lock.json
│   ├── public
│   ├── README.md
│   └── src
|
├── index.js
└── package.json
```

[TOP](#organized-for-deployment)

---

## Development

### API

To develop just the API separately from the frontend run:

* `npm run dev-api`

This will run your api as though it were part of the full live project.  All routes will be have `api/` appended before them and a get request to `/` will return the string `"frontend"`

### Client

To develop just the frontend separately from the API run:

* `npm run dev-client`

> DISCLAIMER!  this will only work if you have set up a mock-api

### Full App

You can also develop the frontend and API in parallel by running:

* `npm run dev`

This script will run the frontend and backend on separate ports, the backend on `localhost:5000` with _nodemon_. The frontend will be run using create-react-app's `start` script, redirecting all API calls to `localhost:5000`.

[TOP](#organized-for-deployment)

---

## Deployment

The main `index.js` in this directory is for deployment. It provides access to your api behind `/api` and statically serves the client from `/client/build`.  You can copy-paste this file directly, there should be need to modify it for your project.

In order for your project to run on Heroku, the main `package.json` needs a `start` command.  This is already taken care of for you.

### Mock

To mock deployment on your local machine you can run these commands.  The app will build and run the same as it will on Heroku to help you troubleshoot your deployed project locally.

* `npm run heroku-postbuild`
* `npm run start`

### Manual

At first you can deploy your project from you local machine.

After creating an account and setting up the Heroku CLI, you can deploy your project by running `git push heroku master` from the top level of your project.

## Automated

It's also possible to configure your Heroku deployment to build from the `master` branch of your github repository each time it is changed.

```
$ heroku create hyf-group6-languageplatform.herokuapp.com   # Create the app
$ heroku git:remote -a hyf-group6-languageplatform.herokuapp.com  # Set `heroku` remote
$ heroku buildpacks:set heroku/nodejs  # Set default language
$ git push heroku infra/setup-heroku:master     # if 'infra/setup-heroku` is the name of local branch
```

[TOP](#organized-for-deployment)

---

## Testing
To locally execute your tests, run the following commands

### Frontend

```bash
cd client
npm install
npm run test:watch
```

### Backend

```bash
cd api
npm install
npm run test:watch
```

## Helpful Links

* [Heroku devhints](https://devhints.io/heroku)
* [Heroku DevCenter: Node.js Support](https://devcenter.heroku.com/articles/nodejs-support)
* [Heroku DevCenter: Advanced Automation](https://devcenter.heroku.com/articles/multiple-environments#advanced-linking-local-branches-to-remote-apps)

[TOP](#organized-for-deployment)

---
---
