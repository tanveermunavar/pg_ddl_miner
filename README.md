# Summary
Scripts to setup DDL logging in the PostgreSQL database using Event Triggers and replicate to the target instance using the golang script.

## Caveats 
PostgreSQL Logical replication does not support DDL replication.So we can use the Events triggers to capture the DDL commands in the source and replicate it to the target replication instance. 

## Usage
git clone https://github.com/tanveermunavar/postgres-ddl-miner.git

cd postgres-ddl-miner/

psql -X -Aqt -h <source_host_ip> -d <source_database> -v ON_ERROR_STOP=1 -f setup_ddl_logging.sql

export GOPATH=\$(go env GOPATH)

/bin/go get -u github.com/lib/pq

/bin/go run logical_replicator.go -shost <source_host_ip> -sdatabase <source_database> -thost <target_host_ip> -tdatabase <target_database>
