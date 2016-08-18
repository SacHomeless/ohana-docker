Docker files to run SacSOS for development.

Prerequisites: Docker. Docker now runs on Windows and Mac, though, as well as Linux.

To use:

 * Clone this repo
 * docker-compose build
 * docker-compose run api bash -l -c "bin/setup"
 * docker-compose up

Then view the site on lvh.me:3001/ for the api, and lvh.me:3000 for the web interface.

To restore a dump of the production data:

 * Add a volume to the pg service with the dump file.
 * Make sure you have the ohana superuser defined. (development uses 'sacsos' instead.)
 * Run pg_restore in the pg service

For example:

    docker-compose run --rm pg bash -l
    su postgres
    createuser --superuser ohana
    pg_restore --dbname ohana_api_development -c /backups/20160814233112_ohana_api_development.psql
