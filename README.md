[![GitHub license](https://img.shields.io/github/license/ethanny2/-postgres-react-node-boilerplate)](https://github.com/ethanny2/-postgres-react-node-boilerplate)
[![GitHub stars](https://img.shields.io/github/stars/ethanny2/-postgres-react-node-boilerplate)](https://github.com/ethanny2/-postgres-react-node-boilerplate/stargazers)
[![GitHub forks](https://img.shields.io/github/forks/ethanny2/-postgres-react-node-boilerplate)](https://github.com/ethanny2/-postgres-react-node-boilerplate/network)
[![Twitter Badge](https://img.shields.io/badge/chat-twitter-blue.svg)](https://twitter.com/ArrayLikeObj)

# Full Stack PERN (PostgreSQL, Express, React, Node) Starter

<p align="center">
  <img width="460" height="300" src="https://repository-images.githubusercontent.com/248812720/56902700-c5bd-11ea-813f-ed8631377258">
</p>

Starting point for making a modern fullstack application with...
- An Express web server
- A PostgreSQL database
- A React front-end

## Local Development

## Prerequisites

You must have a PostgreSQL datbase locally set up on your computer. Here is the offical download page for both Windows and Mac [PostgreSQL Download](https://www.postgresql.org/download/).

Mac users can opt for an even simpler installation by using [Postgres.app](https://postgresapp.com/).

### Setting Up

First, clone this repo locally, then remove the current `.git` folder. Follow this up with making it a new git repo.

```bash
rm -rf .git

git init
```

**Alternatively**: You can download the download the ZIP of this repo to skip this step (git history not included.)

Then go to GitHub, create a new repository, and add that remote to this local repo.

Then, run `npm install` to install all node modules.

You should decide on a name for your local testing database, and edit `db/index.js` changing the value of `DB_NAME`.

This starter uses the Postgres connection URI method to connect to a local Postgres database which you

Once you decide on that name, make sure to run `createdb` from your command line so it exists (and can be connected to).

Finally you can run `npm run server:dev` to start the web server.

In a second terminal navigate back to the local repo and run `npm run client:dev` to start the react server. 

This is set up to run on a proxy, so that you can make calls back to your `api` without needing absolute paths. You can instead `axois.get('/api/posts')` or whatever without needing to know the root URL.

Once both dev commands are running, you can start developing... the server restarts thanks to `nodemon`, and the client restarts thanks to `react-scripts`.

### Project Structure

```bash
├── db
│   ├── index.js
│   └── init_db.js
├── index.js
├── package.json
├── public
│   └── index.html
├── routes
│   └── index.js
└── src
    ├── api
    │   └── index.js
    ├── components
    │   ├── App.js
    │   └── index.js
    └── index.js
```

Top level `index.js` is your Express Server. This should be responsible for setting up your API, starting your server, and connecting to your database, and setting up some basic logging and parsing.

Inside `/db` you have `index.js` which is responsible for creating all of your database connection functions, and `init_db.js` which should be run when you need to rebuild your tables and seed data.

Inside `/routes` you have `index.js` which is responsible for building the `apiRouter`, which is attached in the express server. This will build all routes that your React application will use to send/receive data via JSON.

Lastly `/public` and `/src` are the two puzzle pieces for your React front-end. `/public` contains any static files necessary for your front-end. This can include images, a favicon, and most importantly the `index.html` that is the root of your React application.

### Command Line Tools

In addition to `client:dev` and `server:dev`, you have access to `db:build` which (you will write to) rebuilds the database, all the tables, and seeds in data (once you add it).

## Deployment

### Setting up Heroku (once)

```bash
heroku create 

heroku addons:create heroku-postgresql:hobby-dev
```

This creates a heroku project (with a random name you can change) which will live at https://boiling-inlet-32336.herokuapp.com/ (note, you should change this to be relevant to your project).

It will also create a postgres database for you, on the free tier.

### Getting Ready to Deploy (each time)

Before you deploy you should run the following:

```bash
npm run client:build

git add .

git commit -m "adds front-end of current master to ./build"
```

This will run the `react-script` which will put the entire compiled front-end into the `/build` folder. Our express application serves this folder as if it was a static folder, so that's perfect.

### Deploying

Once you've built the front-end you're ready to deploy, simply run `git push heroku master`. Note, your git has to be clean for this to work (which is why our two git commands live as part of getting ready to deploy, above).

This will send off the new code to heroku, will install the node modules on their server, and will run `npm start`, starting up your express server.

If you need to rebuild your database on heroku, you can do so right now with this command:

```bash
heroku run npm run db:build
```

Which will run `npm run db:build` on the heroku server.

Once that command runs, you can type `heroku open` to get a browser to open up locally with your full-stack application running remotely.
