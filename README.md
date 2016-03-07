# pm2plugin
This plugin will pull data from PM2 and publish to New Relic

# Installation instructions
Make sure you have all of the dependencies (pm2, request, and os)
- Edit package.json and enter your New Relic license key
- You can run app.js using PM2 if you wish
- Data should show up under pm2plugin in your New Relic account

![PM2 Dashboard](/images/pm2dashboard.png)

# Setting up an upstart service

Create the following file `/etc/init/newrelic-pm2.conf`:

```
#!upstart
description "newrelic pm2 monitor"

#start on startup
#stop on shutdown
start on runlevel [2345]

pre-start script
 echo "[`date`] newrelic pm2 monitor starting" >> /opt/pm2/logs/monitor.log
end script

exec node /opt/pm2/newrelic/app.js
```

Change `/opt/pm2/newrelic` to where you have installed the node app, and run `service newrelic-pm2 start` to start it.
