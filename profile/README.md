# SQLRsync
### Built for SQLite
The CDN and version-controlled backup solution for SQLite

Launched October 1st 2025 at [sqlrsync.com](https://sqlrsync.com/)

## Value Proposition
SQLRsync is the only cloud-backed SQLite backup and content distribution system that can be run against running SQLite databases:
- No downtime or write locks in backing up your app's database
- No downtime on read-replicas
- After an initial synchronization, subsequent data transfers only move the modified SQLite Pagedata data: so it's fast, efficient, and great for resource-constrained IoT or edge services.

To support homelab and small projects, users that sign up on https://sqlrsync.com/ unlock 100mb of SQLite storage for life.  (Some terms and conditions apply.)

## Features:
- PUSH and PULL rsync of sqlite3 database files to a remote SQLRsync server (defaults to sqlrsync.com)
- Use `--subscribe` to automatically refresh read-replicas when new data is uploaded
- Creates a [`-sqlrsync` file](https://sqlrsync.com/help/dash-sqlrsync) file neighboring the replicated database which can be shared to PULL down the database elsewhere.
- Stores the PUSH key in ~/.config/sqlrsync/ to allow unattended re-PUSHing of the database (great for a cron job)
- LOCAL Sync (when sqlrsync is provided 2 arguments, both local file paths) allows for a local-only (no server/network use) rsyncing of a running write-node SQLite database to a running read-only SQLite database with no readlocks
- The same mechanism works for PUSH and PULL: the ORIGIN can be a running write-node and the REPLICA can be a running read-only node.  It's pretty magical.

### In PUSH, PULL, or LOCAL mode:
- Use `--dry` to dry-run the command and see what mode it will trigger, and an explanation of what it will do

> <img width="600" height="157" alt="image" src="https://github.com/user-attachments/assets/1988770e-e79d-473a-bd3b-58815dfd6864" />

### When PUSHing:
- On initial upload you can use the `--public` or `--unlisted` flag to allow others to view the webpage for your database, and optionally download any version of it.
- Optionally include a commit message (`--message` or `-m`) to keep track of your changes

### When PULLing:
- You can append an `@` sign and a version reference to download old versions of the database.  For example:
```
sqlrsync oregon/elections.db           # Pulls down the latest version
sqlrsync oregon/elections.db@1         # Pulls down the first version
sqlrsync oregon/elections.db@latest-2  # Goes backwards 2 versions from the latest
```

>  <img width="553" height="74" alt="image" src="https://github.com/user-attachments/assets/1a6608d0-0d66-4801-be98-06ce158f8e6f" />
