## What is this?

The idea of this doc is to provied some instructions on how to setup and
run pg sql.  Additionally, I'm going to leave some additional notes on
things that are worth nothing (ie commands, ways of thinking).
Additionally I would like to include somethings to think about when
deploying (heroku).


Linux users, at the time of writing this, ubuntu ships with an older
version of pg. Don't worry, we'll be installing a newer version


## Who is this for?
This document is aimed at folks with several weeks of experience who
have mostly been using sqlite or other non pg database.


## Installation

### Mac
There are a couple of options for this (homebrew), but while I love to
let homebrew manage all of my apps,
Postgres.app[http://postgresapp.com/] is by far the best way to run pg
on OSX.  Just download it and install it


### Linux
For this I'm going to assume that you are running Ubuntu or something
debian based.

Here is some standard apt stuff we will need to run through.


Update the local package cache
````bash
vagrant@precise32:~$ sudo apt-get update
````

Check to see if there is a version of pg >= 9.2 yet. Don't worry if there
isn't. We'll work around it.

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
`/et/apt/source.list.d/` named pgdg.list. This is where we will be
adding the repo for postgres from the postgres servers. Once the files
have been created, open it in vim and let's add the repo to the source
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
wget --quiet -O - http://apt.postgresql.org/pub/repos/apt/ACCC4CF8.asc |
sudo apt-key add -
```` 

Awesome! We've not got a package repo all setup and ready to go. Update
your apt cache and let's do a search for postgres-9.2 `sudo apt-cache
search postgresql-9.2`  We should now see ~10 pg 9.2 packages and can
now install postgresql like a normal package.

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


## Connecting

Type `psql`



To read more, checkout the postgres wiki
https://wiki.postgresql.org/wiki/Apt





