---
sidebar_position: 50
---

# Add Json into existing SQL table

For example, you already have a customers table in your SQL database. And now you want to add arbitrary key-value pairs into the table. How would you do it?

In this example, your users have multiple customers, and the you have 1 table for all users, and 1 table for all customers in your SQL database.

Your existing schema for the customer table might look like this:

```sql
CREATE TABLE Customers (
    customer_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
    -- other existing columns
);
```

## Database modeling

You can `ALTER` the table to add a new column of metadata with `JSONB` as the type and default value `NULL`. (SQL example for PostgreSQL)

```SQL
ALTER TABLE Customers ADD COLUMN metadata JSONB NULL;
```

Because you are creating a new column, the initial value for the column `metadata` for every row is `null`.

Indexing (Optional): For performance optimization, especially if you plan to query the database based on metadata keys, consider creating GIN (Generalized Inverted Index) indexes on the metadata columns. This is more relevant and supported in PostgreSQL.

```sql
CREATE INDEX idx_customers_metadata ON Customers USING GIN (metadata);
```

You can design the metadata column to store json data to looks like this:

```js
{
  "region": "North America",
  "account_exec_name": "John Doe",
  "tags": ["enterprise", "priority", "2024"]
}
```

## API design

### Base APIs

The plan is to use the `customerId` to update/get the metadata for specific customer id. Since customer id is unique across all the users, there's no need to include `user_id` in this example.

**Endpoint 1**: `PATCH /api/account/customers/{customerId}/metadata`.

Description: Allows adding or updating metadata for a specific customer. The request body should include the metadata key-value pairs to be added or updated. The `PATCH` method is designed for making partial updates to a resource, which includes not only modifying values but also removing them.

Then **design how the request body** for the `PATCH` API to looks like for different purposes. The schema for the API request body is up to you really, just make sure it is consistently use and you handle the backend logic accordingly.

Request body example to update the metadata with new data or to update existing data:

```js
{
  "metadata": {
    "region": "North America",
    "account_exec_name": "John Doe"
  }
}
```

You can also update a specific key, you don't have to make sure the request body has all data every single time. You can also use the same API to add new field to your json metadata.

```js
{
  "metadata": {
    "customer_segment": "Enterprise"
  }
}
```

You can use the same API and use `null` value to indicate that user want to delete the metadata.

```js
{
  "metadata": {
    "account_exec_name": null
  }
}
```

Since simply setting a tag to null wouldn't clearly indicate which tag to remove, a more explicit approach is needed. Specify a clear actions like `add` or `remove` for array elements.

```js
{
  "metadata": {
    "tags": {
      "remove": "priority"
    }
  }
}
```

**Endpoint 2**: `GET /api/account/customers/{customerId}/metadata`.

Description: Retrieves the metadata for a specific customer.

### API to fetch a key from all json

In this example, the customers table has many `customer_id` where every single one is associated with a `user_id`. Let's say you want your user to be able to fetch all `region` key-value pair info from the metadata from all of their customers, you will need another GET API endpoint with `user_id` as one of the path.

**Endpoint 3**: `GET /api/account/{userId}/customers/region`.

Description: This endpoint would return the list of regions for all customers that belong to the specified `user_id`.

MySQL and PostgreSQL both offer JSON support, with PostgreSQL introducing it in version 9.4, including the indexable JSONB datatype, and MySQL starting in version 5.7, complete with a suite of JSON manipulation functions.

For the API implementation, you can use the SQL ORM of your choice, the SQL will look like this:

```sql
SELECT metadata ->> 'region' AS region
FROM Customers
WHERE user_id = :userId
AND metadata ? 'region';
```

- **metadata ->> 'region'** extracts the region value as text from the metadata JSONB column.
- **user_id = :userId** filters the subscriptions to those belonging to the specified user.
- **metadata ? 'region'** ensures that only rows where metadata contains the region key are included in the results.

If your database lacks JSON capabilities or they're not efficient for your needs, you'll have to retrieve and process the entire JSON metadata in your application, leading to more data transfer and higher processing overhead.
