# What?
Originally from my uni project, I dockerised everything and implemented basic features so that we have session/cookie based authentication.
The purpose of this repository is so that, if for any reason, I want to make a brand new application, I have something to fork off of/work off of. Maybe even for hackathons.
This is all of my work.

It works, but is still WIP - there is some clean up required code wise, which I'll eventually get to:
- docker-compose: clean up volumes for frontend (adding new packages), clean up volumes for backend, in particular for maven packages so that it is not installed every time
- improve the code quality/naming of front-end routing
- using authorities instead of role in the backend
- some test endpoints etc need to be removed

# Tech stack
- Bun with Vite, Typescript with React. Tailwind.css for styling. Using tanstack router and tanstack query for routing and querying
- Springboot MVC, using maven
- Redis for auth session storage + distributed systems support for websockets and sessions (Web sockets stuff not implemented yet)
- PostgreSQL for database

# Set up
1. Download pgAdmin4 - this is the UI we will use to access/interact with the postgresDB, should we choose to do so manually. Postgres is a distribution based of SQL, and all the distributions of SQL have their own slight nauances, and as such you'll need specific UIs like pgAdmin4 to configure the DB, access, etc. 
2. Download docker desktop. Then open it.
3. Set up a .env file, and put that file into the root. Create values for DATABASE_NAME, DATABASE_USERNAME, DATABASE_PASSWORD
4. run `docker-compose up --build`. This should start up everything.
5. Connect pgAdmin4 to your postgres db. Create a database as whatever you set DATABASE_NAME to.
6. Copy and paste setup.sql and execute it. This file sets the default admin username and password to be admin and admin respectively.

If you want the cool terminal thing, make sure to install bun, and then run `bun start` from the root.

If you want to use intellij debug mode, make sure to connect the debug to localhost:5005, as that port exposes the bug server. To do this, go to Run/Debug configurations for the main java file, and then select Remote JVM debug.

Every time you make a change to the backend, you need to run `docker-compose up --build` as you need to recompile the backend. 
Every time you add a package to the frontend, you need to run `docker-compose down`, delete the volume associated with the frontend, and then run `docker-compose up --build`. I need to fix this, I'll get to it :D.

It is important that your db schema is up to date. We could use a migration tool to do that for us. Will look into it if I have the time. Nothing wrong with learning some SQL :D.
