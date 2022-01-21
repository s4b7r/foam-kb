# systemctl

## Own service

Used systemctl in [powercontrol-server](https://github.com/s4b7r/powercontrol-server) to create my own service.

## journalctl

```bash
# Just use the journalctl command, as in:

journalctl -u service-name.service

# Or, to see only log messages for the current boot:

journalctl -u service-name.service -b

# For things named <something>.service, you can actually just use <something>, as in:

journalctl -u service-name
```

See https://unix.stackexchange.com/questions/225401/how-to-see-full-log-from-systemctl-status-service
