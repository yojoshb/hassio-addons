This addon creates a proxy to Home Assistant so that you can view the docker processes using: https://github.com/Tecnativa/docker-socket-proxy. This is useful for monitoring Home Assistant docker processes from a remote service/application. 

-   This add-on requires read-only access to the Docker API. It must be ran with **Protection mode** `OFF`

## Security recommendations

-   Never expose this add-on's port to a public network. Only to a Docker networks
    where only reside the proxy itself and the service that uses it.
-   Revoke access to any API section that you consider your service should not need.
-   This image does not include TLS support, just plain HTTP proxy to the host Docker
    Unix socket (which is not TLS protected even if you configured your host for TLS
    protection). This is by design because you are supposed to restrict access to it
    through Docker's built-in firewall.


## Grant or revoke access to certain API sections

You grant and revoke access to certain features of the Docker API through the configuration
variables.

Possible values for these variables:

-   `0` to **revoke** access.
-   `1` to **grant** access.

### Access granted by default

These API sections are mostly harmless and almost required for any service that uses the
API, so they are granted by default.

-   `EVENTS`
-   `PING`
-   `VERSION`
-   `CONTAINERS`

### Access revoked by default

#### Security-critical

These API sections are considered security-critical, and thus access is revoked by
default. Maximum caution when enabling these.

-   `AUTH`
-   `SECRETS`
-   `POST`: When disabled, only `GET` and `HEAD` operations are allowed, meaning any
    section of the API is read-only.

#### Not always needed

You will possibly need to grant access to some of these API sections, which are not so
extremely critical but can expose some information that your service does not need.

-   `BUILD`
-   `COMMIT`
-   `CONFIGS`
-   `ALLOW_START` (containers/`id`/`start`)
-   `ALLOW_STOP` (containers/`id`/`stop`)
-   `ALLOW_RESTARTS` (containers/`id`/`stop`|`restart`|`kill`)
-   `DISTRIBUTION`
-   `EXEC`
-   `GRPC`
-   `IMAGES`
-   `INFO`
-   `NETWORKS`
-   `NODES`
-   `PLUGINS`
-   `SERVICES`
-   `SESSION`
-   `SWARM`
-   `SYSTEM`
-   `TASKS`
-   `VOLUMES`

## Use a different Docker socket location

Home Assistant OS/Supervised uses the default `SOCKET_PATH` of `/var/run/docker.sock`. If your OS stores its Docker socket in a different location and you are unable to bind
mount it in your container specification, you can specify this via the `SOCKET_PATH` configuration variable.

For example, [balenaOS](https://www.balena.io/os/) exposes its socket at
`/var/run/balena-engine.sock`. To accommodate this, merely set the `SOCKET_PATH`
configuration variable to `/var/run/balena-engine.sock`.


## Logging

You can set the logging level or severity level of the messages to be logged with the
configuration variable `LOG_LEVEL`. Default value is info. Possible values are: debug,
info, notice, warning, err, crit, alert and emerg.


## Support

[Open an issue](https://github.com/yojoshb/hassio-addons/issues/new) if you need support. Please do not open issues for this add-on in the main projects repository. 
