MongoDB Extension
This extension provides diagnostic stats from MongoDB(ver >= 3.2)

Download latest release here

Requirements
Infrastructure agent installed
New Relic account
Mongo user with permissions to run diagnostic commands (connPoolStats, serverStatus, dbStats)
MongoDB (ver >= 3.2 )
Installation
Download and untar the latest release
cd to bin
Configure nr-mongodb-ohi-config.yml with your database details (see Configuration section)
Run install.sh
[OPTIONAL] Import dashboard.json via New Relic's dashboard API
The install script takes care of placing the files in the correct directories and restarting the infrastructure agent.

Configuration
Within nr-mongodb-ohi-config.yml, specify the following attributes prior to activating:

mongo_host - The host running mongo (default: localhost)
namespace - namespace that will be string concatinated with the Display and Entity name
mongo_source - The database used to establish credential and priviledges
mongo_db - Comma separated database(s) to obtain stats from (default: admin)
mongo_user - User with permissions to run diagnostic commands on the database
mongo_password - Password of user with permissions to run diagnostic commands
ssl - enable SSL connection (default: false)
pem_key_file - PEM file that contains Private key and Client Certificate
passphrase - passphrase/password used to decrypt the key_file
skip_verify - whether a client verifies the server's certificate chain and host name (default: false). For self signed certificates set to true
If you want to poll multiple hosts/databases from a single host, the configuration file can be set as such. For example:

integration_name: com.nr.mongodb-ohi

instances:
  - name: mongodb-ohi
    command: metrics
    arguments:
      mongo_host: "localhost" #default is localhost or  'localhost:2018' to use a different port
      namespace: "mongo" # default is mongo
      mongo_db: "admin" #comma separated database to get diagnostic info from
      mongo_source: "admin" # database used to establish credentials and privileges
      mongo_user: "<admin_user>" #default is admin
      mongo_password: "<admin_password>"
      ssl: false
      pem_key_file: "<key file>" # PEM file must contain private key & client certificate
      passphrase: "<passphrase>"
      skip_verify: false #whether a client verifies the server's certificate chain and host name

Metric Sets
The following metrics are captured by default- you can get more details around metric descriptions from each command's documentation page:

serverStatus
Asserts
Connections
Global Lock
OpCounters
WiredTiger Storage
Metrics
connPoolStats
dbStats
replSetGetStatus
For a full list of diagnostic commands see this doc.

Event Data
Events will be displayed under the following event types within Insights:

serverStatus: MongoServerStatus
Wired Tiger: MongoWiredTigerStat
connPoolStats: MongoConnectionPoolStat
dbStats: MongoDBStat
replSetGetStatus MongoReplSet
An example dashboard.json is included that can be imported as a starting point for visualizing mongo stats.
