# Cachet provisioning

The [cachet.yml](../cachet.yml) playbook is used to set up the [Cachet](https://cachethq.io/)
status page system. Besides the base system the playbook also uses [a custom monitoring module](https://github.com/mtakaki/cachet-url-monitor),
which monitors websites for outages.

## Setup instructions

Currently Cachet has to be manually set up, since it doesn't expose all the necessary features
for complete automation.

1. Configure [.env](.env) and [monitor-config.yml](monitor-config.yml) to your specifications
1. Start the Cachet service: `docker-compose up cachet`
    * The service will fail after inicialization and ask to set the `APP_KEY` variable.
    * Copy the value and set it in [.env](.env).
1. Restart the Cachet service in the background: `docker-compose up -d cachet`
1. Configure Cachet in the browser (default address is `192.168.5.2:8000`).
    * The recommended settings are as follows:
        * Cache Driver: *APC(u)*
        * Queue Driver: *Synchronous*
        * Session Driver: *APC(u)*

1. Add appropriate components and metricts (based on your `monitor-config.yml`)
1. Create a new team member for the monitoring module (optional - alternatively use the main user)
1. Copy a team member's API Token (accessible from `/dashboard/user` on the website) and set it in [.env](.env) as the
    `CACHET_TOKEN`
1. Start the monitoring module's service: `docker-compose up -d module`
