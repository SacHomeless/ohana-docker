Docker files to run SacSOS for development.

Prerequisites: Docker. Docker now runs on Windows and Mac, though, as well as Linux.

To use:

 * Clone this repo
 * docker-compose build
 * docker-compose run api bash -l -c "bin/setup"
 * docker-compose up

Then view the site on lvh.me:3001/ for the api, and lvh.me:3000 for the web interface.
