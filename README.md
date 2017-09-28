reproduces a bug in sequelize 3 and 4

### repro steps:

```
yarn
node_modules/.bin/sequelize db:create
node_modules/.bin/sequelize db:migrate
```

### expected:

the second migration succeeds

### actual:

```
vagrant@vagrant-ubuntu-trusty-64:~/projects/sequelize-err-on-rename-repro$ ./node_modules/.bin/sequelize db:migrate

Sequelize CLI [Node: 8.6.0, CLI: 3.0.0, ORM: 4.11.1]

WARNING: This version of Sequelize CLI is not fully compatible with Sequelize v4. https://github.com/sequelize/cli#sequelize-support

Loaded configuration file "config/config.json".
Using environment "development".
== 20170928040207-remove-email-column: migrating =======
Unhandled rejection SequelizeDatabaseError: Error on rename of './sequelize_err_on_rename_repro/Users' to './sequelize_err_on_rename_repro/#sql2-45c-1c4' (errno: 152)
    at Query.formatError (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/sequelize/lib/dialects/mysql/query.js:222:16)
    at Query.connection.query [as onResult] (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/sequelize/lib/dialects/mysql/query.js:55:23)
    at Query.Command.execute (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/mysql2/lib/commands/command.js:30:12)
    at Connection.handlePacket (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/mysql2/lib/connection.js:515:28)
    at PacketParser.onPacket (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/mysql2/lib/connection.js:94:16)
    at PacketParser.executeStart (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/mysql2/lib/packet_parser.js:77:14)
    at Socket.<anonymous> (/home/vagrant/projects/sequelize-err-on-rename-repro/node_modules/mysql2/lib/connection.js:102:29)
    at emitOne (events.js:115:13)
    at Socket.emit (events.js:210:7)
    at addChunk (_stream_readable.js:266:12)
    at readableAddChunk (_stream_readable.js:253:11)
    at Socket.Readable.push (_stream_readable.js:211:10)
    at TCP.onread (net.js:587:20)

== 20170928040207-remove-email-column: migrated (0.031s)

```
