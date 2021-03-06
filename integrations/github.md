---
title: Github Integration
tags: [integrations list]
permalink: github.html
summary: Learn about the Wavefront Github Integration.
---
## Github Integration
GitHub is a web-based hosting service for version control using Git. It offers the distributed version control and source code management functionality of Git and adds access control and collaboration features.

This integration installs and configures Telegraf to send Github metrics into Wavefront. Telegraf is a light-weight server process capable of collecting, processing, aggregating, and sending metrics to a [Wavefront proxy](https://docs.wavefront.com/proxies.html).

In addition to setting up the metrics flow, this integration installs a dashboard. Here are the **Overview** and **Events** sections of a dashboard displaying Github metrics:

{% include image.md src="images/overview.png" width="80" %}


To see a list of the metrics for this integration, select the integration from <https://github.com/influxdata/telegraf/tree/master/plugins/inputs>.
## Github Setup



### Step 1. Install the Telegraf Agent
This integration uses the Webhooks input plugin for Telegraf. If you've already installed Telegraf on your server(s), you can skip to Step 2.

Log in to your Wavefront instance and follow the instructions in the **Setup** tab to install Telegraf and a Wavefront proxy in your environment. If a proxy is already running in your environment, you can select that proxy and the Telegraf install command connects with that proxy. Sign up for a [free trial](http://wavefront.com/sign-up/?utm_source=docs.vmware.com&utm_medium=referral&utm_campaign=docs-front-page){:target="_blank" rel="noopenner noreferrer"} to check it out!

### Step 2. Configure the Telegraf Webhooks input plugin

Create a `webhooks.conf` file in `/etc/telegraf/telegraf.d` and add the following snippet:

 {% raw %}
```   
   #   ## A Webhooks Event collector
   [[inputs.webhooks]]
   #   ## Address and port to host Webhook listener on
       service_address = ":1619"
   #
      [inputs.webhooks.github]
         path = "/github"
```
{% endraw %}
See the [Telegraf documentation](https://github.com/influxdata/telegraf/tree/master/plugins/inputs/webhooks) for details.

### Step 3. Restart Telegraf

Run `sudo service telegraf restart` to restart your Telegraf agent.

### Step 4. Configure Github Webhooks Services

To capture metrics from Github you should configure your Organization's Webhooks to point at the webhooks service. To do this:

1. Go to github.com/{my_organization} and click **Settings > Webhooks > Add webhook.**
2. Set **Payload URL** to `http://hostIP:1619/github`
3. Set **Content type** to `application/json`.
4. Select **Send me everything**.
