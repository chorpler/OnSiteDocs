# Setting up CouchDB
## To create user for CouchDB in Fedora/RHEL/CentOS:
```bash
adduser --system --home /home/couchdb --no-create-home --shell /bin/bash --user-group --comment "CouchDB Administrator" couchdb
```
## When CouchDB is running and needs first databases created:
```bash
curl -X PUT http://127.0.0.1:5984/_users
curl -X PUT http://127.0.0.1:5984/_replicator
curl -X PUT http://127.0.0.1:5984/_global_changes
```
or, when not in admin party mode:
```bash
curl -X PUT --user ${USER}:${PASSWORD} http://127.0.0.1:5984/_users
curl -X PUT --user ${USER}:${PASSWORD} http://127.0.0.1:5984/_replicator
curl -X PUT --user ${USER}:${PASSWORD} http://127.0.0.1:5984/_global_changes
```

## To create CouchDB service
- Put the following in `couchdb/etc/couchdb.service`:
  ```
  [Unit]
  Description=CouchDB service
  After=network.target
  
  [Service]
  Type=simple
  User=couchdb
  #ExecStart=/couchdb/bin/couchdb -o /dev/stdout -e /dev/stderr
  ExecStart=/couchdb/bin/couchdb
  Restart=always
  
  [Install]
  WantedBy=multi-user.target
  ```

- Symlink to it in the `systemd` directory:
  ```bash
  ln -s /couchdb/etc/couchdb.service /etc/systemd/system/couchdb.service
  ```

- Run `systemd` commands to enable it to start up automatically:
  ```bash
  systemctl daemon-reload
  systemctl start couchdb.service
  systemctl enable couchdb.service
  ```

