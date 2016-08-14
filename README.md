Docker files to run SacSOS for development.

Currently very basic. It runs ohana-api, but not yet ohana-client.

Prerequisites: Docker. Docker now runs on Windows and Mac, though, as well as Linux.

To use:

 * Clone this repo
 * docker-compose build
 * docker-compose run api bash -l -c "bin/setup"
 * docker-compose up

Then view the site on localhost:3001/
