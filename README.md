YSA.LOGROTATE
=========
Installing and configuring logrotate.

[![SWUbanner](https://raw.githubusercontent.com/vshymanskyy/StandWithUkraine/main/banner2-direct.svg)](https://github.com/vshymanskyy/StandWithUkraine/blob/main/docs/README.md)

Role Variables
--------------
```yaml
# Install logrotate package
logrotate_install: true

# Rewrite default logrotate config
# By default:  (see vars/%OS%.yml
# logrotate_options:
#   - weekly
#   - rotate 4
#   - copytruncate
#   - dateext
#   - compress
logrotate_options: [ ]

# Logrotate configs dir path
logrotate_include_dir: /etc/logrotate.d

# Removing all configs in the {{logrotate_include_dir}} before deploy
logrotate_cleanup_configs: false

# Adds rotation configs for wtmp and btmp logs
# As a rule, currently, all packages add this config by default, if needed to enable
logrotate_enable_wtmp_rotate: false
logrotate_enable_btmp_rotate: false

logrotate_logs: [ ]

```

Example
----------------

```yaml
logrotate_logs:
   - name: app-logs
     paths:
       - /srv/my-app/logs/app-production.log
       - /srv/my-app/logs/worker-production.log
     options:
       - rotate 6
       - monthly
       - missingok
       - notifempty
       - compress
     firstaction: 
       - rm -rf /
     lastaction: 
       - /usr/local/bin/lastaction.sh
     prerotate: 
       - /usr/local/bin/prerotate.sh
     postrotate: 
       - /usr/local/bin/postrotate.sh
```

License
-------
[MIT](./LICENSE.md)

