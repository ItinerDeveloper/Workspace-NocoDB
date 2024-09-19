# NocoDB Data Insertion Service

## Prerequisite
The Workspace application must be integrated with NocoDB. NocoDB is a no-code database platform with a spreadsheet-like user interface.

## Service Route
`TBD`

## Description
The service allows data to be sent from a workflow to NocoDB via a webhook. The service retrieves the name of the table where the data should be inserted from the Workspace template variable `nocodbTable`. It then searches for variables in the workflow that match the field names of the specified NocoDB table and assembles a record based on these variables. The assembled record is subsequently saved to the appropriate table in NocoDB.

## Dedicated Template Variable
- **nocodbTable**: The name of the NocoDB table where the data will be inserted.

## Further Information
For more information about NocoDB, please visit the [NocoDB Website](https://nocodb.com/#How-it-works).

---

This service is part of the Itiner Workspace integrations and is designed to facilitate seamless data insertion into NocoDB from within your workflows.
