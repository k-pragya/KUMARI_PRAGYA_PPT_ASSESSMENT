Task 17: DynamoDB Table Creation

Objective
Create a NoSQL table in Amazon DynamoDB using partition and sort keys, and insert sample items.

Steps
1. Create Table

Opened AWS Console → DynamoDB → Create Table.
Table Name: Dynamo2
Primary Keys:
Partition Key: UID (Number)
Sort Key: OID (Number)
Used default settings (On-demand mode).
Created table and waited for status Active.

2. Insert Items

Opened Dynamo2 → Items → Create Item.
Item 1:
UID: 1
OID: 100
item1: "SampleData1"
Saved items successfully.

3. Verification

Confirmed table status is Active.
Verified UID and OID as primary keys.
Checked inserted items in the Items tab.

Outcome

Dynamo2 table created successfully.
Primary keys configured correctly.
Sample items inserted and ready for use.