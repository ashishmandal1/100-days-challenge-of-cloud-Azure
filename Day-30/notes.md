# Day 30 - Azure SQL Database

## Objective
Created a publicly accessible Azure SQL Database with Basic compute and locally redundant backup storage.

## Resources Created
- SQL Server: `nautilus-server-14089`
- SQL Database: `nautilus-sqldb`

## Configuration
- Region: `westus`
- Administrator: `nautilus-admin`
- Public Network Access: Enabled
- Compute Tier: Basic
- Capacity: 5 DTUs
- Maximum Database Size: 2 GiB
- Backup Storage Redundancy: Local
- Database Status: Online
- Server State: Ready

## Verification
Verified the SQL database and server using Azure CLI.

Database:
`nautilus-sqldb` → Online

Server:
`nautilus-server-14089` → Ready

## Result
Successfully created and verified the required publicly accessible Azure SQL Database.