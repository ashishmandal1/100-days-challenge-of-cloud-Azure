# Day 41 - Azure Table Storage

## Task

Created an Azure Storage Account with an Azure Table Storage table and inserted task entities using Azure CLI.

## Resources Created

* Storage Account: `devopstablest131188897`
* Table: `tasks`
* Region: `eastus`
* Resource Group: `kml_rg_main-a60a79fcda9c4540`

## Table Entities

### Task 1

* PartitionKey: `tasks`
* RowKey: `1`
* Description: `Learn Table Storage`
* Status: `completed`

### Task 2

* PartitionKey: `tasks`
* RowKey: `2`
* Description: `Build To-Do App`
* Status: `in-progress`

## Verification

Both entities were queried successfully using Azure CLI.

Task 1 status verified:
`completed`

Task 2 status verified:
`in-progress`

## Status

Day 41 completed successfully.
