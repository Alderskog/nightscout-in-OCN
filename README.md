# nightscout-in-OCN, Caddy as reverse Proxy

This is a collection of files documenting a working deployment of Nightscout (main). I've used an Oracle Cloud server, ARM-compute instance with Ubuntu 22.04.2 (GNU/Linux 5.15.0-1038-oracle aarch64). The process should be more or less platform independent.

Nightscout:

Nightscout is deployed with docker compose, similar to the official docker-compose.yml but with environment variables in a separate .env file. I've also dropped the Traefik reverse proxy; I've been using Caddy simple because it's easier to set up. On top of this, Authentik for authentication with single sign-on to other services. 

For using this you will need to edit the .env file:
* API_SECRET: make up your own
* MONGODB_URI: paste the URI of your Atlas MongoDB database or comment this out if using a local database
* MONGO_CONNECTION: uncomment if you use the local database
* PAPERTRAIL_API_TOKEN: paste your API token from Atlas MongoDB or comment out if irrelevant

If you run with an external Atlas MongoDB database, the mongodb can of course be removed from docker-compose.yml

Caddy:

Caddy can be deployed as a docker container but I opted for installing directly to host per these instructions:
https://caddyserver.com/docs/install#debian-ubuntu-raspbian

I can't recommend Caddy more for a reverse proxy. If serving as nothing more than a reverse proxy for nightscout on port 1337, these 3 lines would suffice: 
nightscout.domain.com {
	reverse_proxy localhost:1337
}

Basic config really is that simple. 

Authentik:
An authorization platform is probably not as important as the reverse proxy. Deploying with docker compose was simple enough with the official instructions:
https://goauthentik.io/docs/installation/docker-compose

Config was more difficult, personal documentation pending.
