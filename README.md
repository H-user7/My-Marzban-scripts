# Marzban-scripts
Scripts for [H-user7/My-Marzban](https://github.com/H-user7/My-Marzban).

Installation downloads the panel's `master` branch and builds `my-marzban:local`
on your server using the fork's Dockerfile. No published panel image is required.
Push your panel changes to GitHub before installing or updating a server; local
uncommitted changes are not included. Source downloads require a publicly readable
repository. The build needs internet access and can take several minutes.

Configuration stays in `/opt/marzban/.env`, panel source is managed in
`/opt/marzban/source`, and persistent data stays in `/var/lib/marzban`.

## Updating your panel

```bash
sudo marzban update
```

This downloads and rebuilds the selected branch or tag from your panel fork before
restarting services. Existing `.env`, Xray configuration, database settings and
volumes are preserved. `--dev` uses your fork's `dev` branch; `--version` uses a tag
from your fork. Those refs must exist there. Updates keep the selection made at
installation; the default `latest` follows `master`.

To switch an existing upstream installation to this fork, first install this
management script, then update:

```bash
sudo bash -c "$(curl -fsSL https://raw.githubusercontent.com/H-user7/My-Marzban-scripts/master/marzban.sh)" @ install-script
sudo marzban update
```

Existing installations without a saved source selection switch to your fork's
`master` branch. The panel's Compose service is changed to a local source build;
other service settings are retained. A failed download or build stops the update
before services are stopped.

The node management script also updates from this scripts repository. Its node
container continues to use `gozargah/marzban-node`, since this fork customizes the
panel.

## Installing Marzban

- **Install Marzban with SQLite**:

```bash
sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban.sh)" @ install
```

- **Install Marzban with MySQL**:

  ```bash
  sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban.sh)" @ install --database mysql
  ```

- **Install Marzban with MariaDB**:

  ```bash
  sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban.sh)" @ install --database mariadb
  ```
  
- **Install Marzban with MariaDB and your fork’s dev branch**:

  ```bash
  sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban.sh)" @ install --database mariadb --dev
  ```

- **Install Marzban with MariaDB and a tag from your fork**:

  ```bash
  sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban.sh)" @ install --database mariadb --version v0.8.4
  ```

- **Update or Change Xray-core Version**:

  ```bash
  sudo marzban core-update
  ```


## Installing Marzban-node
Install Marzban-node on your server using this command
```bash
sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban-node.sh)" @ install
```
Install Marzban-node on your server using this command with custom name:
```bash
sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban-node.sh)" @ install --name marzban-node2
```
Or you can only install this script (marzban-node command) on your server by using this command
```bash
sudo bash -c "$(curl -sL https://github.com/H-user7/My-Marzban-scripts/raw/master/marzban-node.sh)" @ install-script
```

Use `help` to view all commands:
```marzban-node help```

- **Update or Change Xray-core Version**:

  ```bash
  sudo marzban-node core-update
  ```
