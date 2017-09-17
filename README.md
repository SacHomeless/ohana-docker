## Docker files for SacSOS development.

Prerequisites: Docker. Git. Bash.

To use:

Clone this repo, along with sacsos api and sacsos web, into subdirectories
of the same directory. Then build and run:

```bash
git clone git@github.com:SacHomeless/ohana-api.git
git clone git@github.com:SacHomeless/ohana-docker.git
git clone git@github.com:SacHomeless/ohana-web-search.git
cd ohana-api
git checkout add_search_orgs_locations
cd ../ohana-docker
docker-compose build
docker-compose exec api bash -l -c "rake db:setup"
docker-compose exec api bash -l -c "bin/setup"
docker-compose up
```

Then view the site on lvh.me:3001/ for the api, and lvh.me:3000 for the web interface.

*Note:* lvh.me is a normal domain that resolves to 127.0.0.1.
So it always refers to your local machine.

## Running etc

See the [docker-compose help](https://docs.docker.com/compose/reference/). Or

```bash
docker-compose help
```

Start everything running:

```bash
docker-compose up
```

Stop everything

```bash
docker-compose stop
```

## Loading a copy of production data

First, add a volume to the pg container definition in docker-compose.yml to let you read the
dumped database file from within the pg container

```yaml
  pg:
    image: postgres
    environment:
      - POSTGRES_PASSWORD=password1
      - POSTGRES_USER=sacsos
    volumes:
      - ../backup/backup/backups:/backups/:z
```

*Note:* the `:z` suffix on the volume line is needed for Fedora, and has to do with SELinux
permissions; if you're not using Fedora, you probably don't need it.

Then make sure you have a clean database. If you've run `rake db:setup`
and `bin/setup`, you'll need to drop the database and start over.
It may be easiest to recreate the docker container:

```bash
docker-compose stop
docker-compose up --force-recreate
```

Then, in another terminal:

```bash
docker-compose exec pg bash -l
su postgres
psql < path_to_dump_file
```
