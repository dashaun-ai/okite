# Okite

Okite (掟, “rules”) is the versioned, non-secret runtime configuration repository served by Sashizu
to the dashaun-ai applications.

Files follow Spring Cloud Config naming: `application.yml` applies to every client,
`<application>.yml` applies to one service, and `<application>-<profile>.yml` applies when that
profile is active.

Never commit credentials, signing keys, OAuth client secrets, API keys, or passwords. Those remain
platform-provided environment variables or service-binding credentials.

After pushing a configuration change, GitHub should POST its push webhook to Sashizu `/monitor`.
Config Monitor publishes a targeted event on the `sashizu.config` RabbitMQ bus; connected clients
then rebind refreshable configuration without a restart.
