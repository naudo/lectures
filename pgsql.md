## What is this?

The idea of this doc is to provide some instructions on how to setup and
run Postgres.  Additionally, I'm going to leave some additional notes on
concepts / features that are important to understand Postgres.  Deployment will be covered.

Linux users, at the time of writing this, ubuntu ships with an older
version of pg. Don't worry, we'll be installing a newer version.


## Who is this for?
This document is aimed at folks with several weeks of programming /database experience who
have mostly been using sqlite or other non pg databases.  I'm going to assume that you know 
how to (look up) the syntax for sql stuff such as creating a table and querying.  I will point 
terminal commands that may be new.


## Installation

### Mac
I generally advocate just installing programs through homebrew (http://brew.sh/) but there
is an amazing mac app that is already built.  Just download Postgres.app (http://postgresapp.com/)
and drag / drop it to your Applications folder.  Starting Postgres.app will put an elephant icon in
your system tray.

### Linux
For this I'm going to assume that you are running Ubuntu or something
debian based.

Here is some standard apt stuff we will need to run through.


Update the local package cache
````bash
vagrant@precise32:~$ sudo apt-get update
````

Check to see if there is a version of pg >= 9.2 yet. If there is, feel 
free to skip ahead to installing with apt. If it doesn't exist, Don't 
worry, we'll work around it. 

```bash
vagrant@precise32:~$ sudo apt-cache search postgresql | grep postgresql-9.
````
This will spit out a bunch of different packages. The key thing of what
we're looking for is postgresql-9.2.  If it's not there (older verions
of ubuntu ship with 9.1 or even just 8.4) move onto the next step. If
9.2 is present, skip ahead to the installation step.

### Adding new packages
The underpinnings of Linux can be incredibly simple. Remember how when
we typed in `sudo apt-get update` how a whole bunch of urls appeared?
Did you wonder where those came from, or what they did?  Turns out the
the aptitude package manager (or apt) is powered by a text file. That's
right. The thing that tells your computer where to download an install
files from is defined in several different files.  Default ubuntu packages go into `/etc/apt/sources.list` which is great, except for one thing,
the packages we want don't exist in the main ubuntu repos yet.
Foruntately we can add more. Create a new file in
`/et/apt/source.list.d/` named `pgdg.list`. This is where we will be
adding the repo for postgres from the postgres project's servers. Once the file
has been created, open it in vim and let's add the repo to the source
file.
````
deb http://apt.postgresql.org/pub/repos/apt/ precise-pgdg main
````

The abilty to add packages from any server is incredibly powerful. While
this can be a good thing, we also need to make sure that a repo is safe
before we start installing random programs onto our machines.  To help,
let's go ahead and download the repo key for postgres.  Run the
following command from the command line to download and add the key.

````
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc | sudo apt-key add -
```` 

Awesome! We've got the package repo all setup and ready to go. Update
your apt cache and let's do a search for postgres-9.2 `sudo apt-cache
search postgresql-9.2`  We should now see ~10 pg 9.2 packages and can
now install postgresql via apt.

### Installing from apt

After running you should see some info printed out. This tells you a
little bit about your brand new pg data (like what port it will listen
on and where the data is being stored).

````
...
Creating new cluster 9.2/main ...
  config /etc/postgresql/9.2/main
  data   /var/lib/postgresql/9.2/main
  locale en_US
  port   5432
...
````


Congrats! You should now be ready to connect

To read more, checkout the postgres wiki
https://wiki.postgresql.org/wiki/Apt



## Connecting

Type `psql`. Chances are if you just installed from apt, you'll get an
error that looks similar to 

````bash
vagrant@precise32:~$ psql
psql: FATAL:  role "vagrant" does not exist
````

Ugh,  a roadblock.  Worry not because this leads into our first
postgres lesson about roles.



### Roles

WRITE ME PLOX


### Connecting( for real this time!)
So now that we've learned about roles, let's connect to the db

````bash
vagrant@prcise32:~$ sudo -u postgres psql postgres
psql (9.2.4)
Type "help" for help.

postgres=# 
````

Yea, we now have database access and are inside of postgres! Feel free to write
some queries to play around with it


### Creating a DB

So we've installed, setup, and connected to postgres. You may be
surprised to learn that we don't actually have a DB yet and will have to
create it. Fortunately postgres comes with a command to do just this.
Run the following command, replacing mydb with what you would like to
name your database.

```bash
 sudo -u postgres createdb mydb
````

Awesome! Now that we're all setup with postgres and have created our database,
it's time to start hacking.

## Configuring SQL Alchemy & Flask

add some stuff to requirements.txt `psycopg2==2.5`


## Deploying
Deal with taking an existing heroku app, and making the neccesarry changes
to allow it to run on heroku. Don't need to worry about explaining how heroku
works or to use it.
//Check that the add on exists
//if it doesn't add it

Heroku exposes through env var `DATABASE_URL`. Let's connect to this.

Great! it works, but what happens if we want to delete a table and test some 
code? Or what if we want to create a user but not let them login to the production site yet?

### Different evniornments

## Misc

###Helpful commands
WRITE ME PLOX



##More links
http://www.lainoox.com/apt-get-packages/
