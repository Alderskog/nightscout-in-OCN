# nightscout-in-OCN

This is a collection of files documenting a working deployment of Nightscout (main). I've used an Oracle Cloud server, ARM-compute instance with Ubuntu 22.04.2 (GNU/Linux 5.15.0-1038-oracle aarch64).

Nightscout is deployed with docker compose, similar to the official docker-compose.yml but with environment variables in a separate .env file. I've also dropped the Traefik reverse proxy; I've been using Caddy simple because it's easier to set up. On top of this, Authentik for authentication with single sign-on to other services. 

For using this you will need to edit the .env file:
* API_SECRET: make up your own
* MONGODB_URI: paste the URI of your Atlas MongoDB database or comment this out if using a local database
* MONGO_CONNECTION: uncomment if you use the local database
* PAPERTRAIL_API_TOKEN: paste your API token from Atlas MongoDB or comment out if irrelevant

If you run with an external Atlas MongoDB database, the mongodb can of course be removed from docker-compose.yml
