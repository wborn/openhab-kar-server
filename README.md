# openhab-kar-server

This is a proof of concept for creating an online KAR repository based on exploded KAR files.

## Adding content

Content can be added to the repository using the `./add-kars` script.
The script can install pre-downloaded KAR files as well as download and install existing openHAB KAR files.
When KARs are added, the script also generates SHA1 checksum files which are used by Aether to check downloaded content for corruption.

### Adding pre-downloaded KAR files

To install pre-downloaded KARs execute: `./add-kars <karfiles>`

If you've downloaded several KAR files to the `kars/` directory you can for instance add them all using: `./add-kars kars/*`

### Adding downloaded KAR files

The script can also download existing openHAB KAR files and then add these to the KAR repo.

For instance to add some release, milestone and snapshot KARs execute:

```bash
./add-kars 3.1.0 3.2.0.M4 3.2.0-SNAPSHOT
```

To install all currently downloadable KARs execute:

```bash
./add-kars 2.3.0 2.4.0 2.5.0 2.5.12 3.0.0 3.0.1 3.0.2 3.1.0 3.1.0.M3 3.1.0.M4 3.1.0.M5 3.1.0.RC1 3.2.0.M1 3.2.0.M2 3.2.0.M3 3.2.0.M4 3.2.0-SNAPSHOT
```

## Serving content

Depending on the release type, the KARs are added to the following repository directories:

* libs-milestone
* libs-release
* libs-snapshot

These repository directories can be served as static content by any webserver.

There is an example `docker-compose.yml` file available that serves the content using an NGINX Docker container on port 80.

To start this container execute: `docker-compose up -d`

## Downloading content

To download artifacts from the KAR repository server the openHAB `userdata/etc/org.ops4j.pax.url.mvn.cfg` file needs to be updated.

For instance when using the NGINX container you can update it for openHAB release versions to:

```
org.ops4j.pax.url.mvn.repositories= \
	http://localhost/libs-release@id=openhab
```
