## Install PostgreSQL

### Install PostgreSQL on Ubuntu

**Step 1. Add PostgreSQL Repository**

You can use the apt command to install it on ununtu
```bash
apt install postgresql
```

**OR**

If the version included in your version of Ubuntu is not the one you want, you can use the PostgreSQL Apt Repository.

The `PostgreSQL Apt Repository` supports the current versions of Ubuntu:

* noble (24.04, LTS)
* mantic (23.10, non-LTS)
* jammy (22.04, LTS)
* focal (20.04, LTS)

on the following architectures:

* amd64
* arm64 (LTS releases only)
* ppc64el (LTS releases only)
* s390x (LTS releases only)

**Automated repository configuration:**

```bash
sudo apt install -y postgresql-common
sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
```
[Check out this for more information](https://www.postgresql.org/download/linux/ubuntu/)

**Step 2. Install PostgreSQL 16**

First, install PostgreSQL and its contrib modules:
```bash
sudo apt install postgresql-16 postgresql-contrib-16
```

Second, start the PostgreSQL service:
```bash
sudo systemctl start postgresql
```

Third, enable PostgreSQL service:
```bash
sudo systemctl enable postgresql
```

**Step 3. Configure PostgreSQL server**

By default, only connections from the local system are allowed. To enable all other computers to connect to your PostgreSQL server, edit the file `/etc/postgresql/*/main/postgresql.conf`. 
```bash
sudo nano /etc/postgresql/16/main/postgresql.conf
```

Locate the line: `#listen_addresses = ‘localhost’` and change it to`*`:
```bash
listen_addresses = '*'
```

Note:
`‘*’` will allow all available IP interfaces (IPv4 and IPv6), to only listen for IPv4 set 0.0.0.0 while `‘::’` allows listening for all IPv6 addresses.

[For more check out this](https://ubuntu.com/server/docs/install-and-configure-postgresql)

Configure PostgreSQL to use md5 password authentication in the `pg_hba.conf` file. This is necessary if you want to enable remote connections.
```bash
sudo sed -i '/^host/s/ident/md5/' /etc/postgresql/16/main/pg_hba.conf
sudo sed -i '/^local/s/peer/trust/' /etc/postgresql/16/main/pg_hba.conf
echo "host all all 0.0.0.0/0 md5" | sudo tee -a /etc/postgresql/16/main/pg_hba.conf
```

Restart PostgreSQL for the changes to take effect.
```bash
sudo systemctl restart postgresql
```

Allow PostgreSQL port through the firewall.
```bash
sudo ufw allow 5432/tcp
```

**Connect to the PostgreSQL database server**

First, connect to the PostgreSQL server using the postgres user:
```bash
sudo -u postgres psql
```

Second, set a password for postgres user:
```bash
ALTER USER postgres PASSWORD '<password>';
```
Replace the `<password>` with the one you want.

Third, quit the psql:
```bash
\q
```

**Install pgAdmin**

To install pgAdmin4 on ubuntu, first we need to add the public key of the repository.
```bash
curl -fsS https://www.pgadmin.org/static/packages_pgadmin_org.pub | sudo gpg --dearmor -o /usr/share/keyrings/packages-pgadmin-org.gpg
```

Now we need to create the configuration file
```bash
sudo sh -c 'echo "deb [signed-by=/usr/share/keyrings/packages-pgadmin-org.gpg] https://ftp.postgresql.org/pub/pgadmin/pgadmin4/apt/$(lsb_release -cs) pgadmin4 main" > /etc/apt/sources.list.d/pgadmin4.list && apt update'
```
Now it's time to install the application itself.
```bash
sudo apt install pgadmin4-desktop
```


Congratulations! You have successfully installed PostgreSQL and pgAdmin4 on Ubuntu.
