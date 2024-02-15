# Database Migration

## When do we need to do database migration?

Database migration, particularly the process of creating a new table and migrating data from an old table to the new one, is typically required in several scenarios, including but not limited to:

1. **Schema Redesign**: When the initial database schema no longer meets the application's requirements due to changes in business logic, performance issues, or scalability concerns.

2. **Normalization/Denormalization**: Adjusting the database structure for optimization purposes, either by normalizing data to reduce redundancy and improve data integrity, or by denormalizing to improve query performance.

3. **Technology Upgrade**: Moving to a new database system or version that supports better features or performance, requiring a redesign of the existing tables.

4. **Feature Addition**: Introducing new features that require significant changes to the database schema, including new relationships or data types that weren't previously considered.

## Example

Let's consider a hypothetical scenario involving a `Customers` table where the initial schema no longer meets the application's evolving requirements, necessitating a redesign and migration to a new schema. I'll provide a before and after example, highlighting the types of changes that might necessitate such a migration.

### Initial Schema: Before Redesign

The initial `Customers` table might look something like this:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    Name VARCHAR(100),
    Email VARCHAR(100) UNIQUE,
    Address VARCHAR(255),
    PhoneNumber VARCHAR(15),
    RegistrationDate DATE
);
```

In this schema, the `Customers` table includes basic information: a unique customer ID, name, email, address, phone number, and the date they registered.

### Reasons for Redesign

As the application grows, you might encounter several reasons to redesign this table:

1. **Normalization**: Splitting the `Address` into multiple fields (e.g., street, city, state, zip code) for more precise querying and reporting.
2. **Performance Optimization**: Adding indexes on columns frequently used in searches.
3. **New Features**: Supporting multiple phone numbers and emails for a single customer.
4. **Compliance and Security**: Adding fields for consent management due to privacy regulations like GDPR.
5. **Data Type Changes**: Adjusting data types for better efficiency or to accommodate larger values.

### Redesigned Schema: After Redesign

The redesigned `Customers` table, incorporating these changes, could look like this:

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    FirstName VARCHAR(100),
    LastName VARCHAR(100),
    -- Splitting Email and PhoneNumber into their own tables for supporting multiples
    RegistrationDate DATE,
    Street VARCHAR(255),
    City VARCHAR(100),
    State VARCHAR(50),
    ZipCode VARCHAR(10),
    -- New columns
    ConsentGiven BOOLEAN DEFAULT FALSE,
    ConsentDate DATE
);

CREATE TABLE CustomerEmails (
    EmailID INT PRIMARY KEY,
    CustomerID INT,
    Email VARCHAR(100) UNIQUE,
    IsPrimary BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);

CREATE TABLE CustomerPhoneNumbers (
    PhoneID INT PRIMARY KEY,
    CustomerID INT,
    PhoneNumber VARCHAR(15),
    IsPrimary BOOLEAN DEFAULT FALSE,
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

### Changes Explained:

- **Normalization**: The address is split into `Street`, `City`, `State`, and `ZipCode` for more detailed geographic segmentation and analysis.
- **Supporting Multiple Contacts**: By moving `Email` and `PhoneNumber` to separate tables (`CustomerEmails` and `CustomerPhoneNumbers`), the new design supports multiple emails and phone numbers per customer, including flags for primary contacts.
- **Data Integrity and Relationship Management**: The use of foreign keys (`FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)`) ensures data integrity between the `Customers` table and the new `CustomerEmails` and `CustomerPhoneNumbers` tables.
- **Compliance and Security**: Added `ConsentGiven` and `ConsentDate` to manage privacy consent status, addressing potential regulatory requirements.
- **Name Splitting**: Splitting `Name` into `FirstName` and `LastName` facilitates more flexible data handling and reporting.

### Migration Process:

The migration from the old schema to the new one would involve:

1. Creating the new tables (`Customers`, `CustomerEmails`, `CustomerPhoneNumbers`).
2. Migrating existing data, which may include splitting full names and addresses into their new respective fields and distributing primary emails and phone numbers into their new tables.
3. Implementing new application logic to interact with the updated schema.
4. Testing thoroughly to ensure data integrity and application functionality.

This process would be planned and executed carefully to minimize downtime and data loss, often involving temporary tables or scripts to transform data as needed.

## Migration Steps

1. **Plan**: Analyze current schema, design new schema, plan strategy.
2. **Prepare**: Backup data, prepare scripts, set up staging.
3. **Test**: Execute in staging, test functionality, adjust as needed.
4. **Execute**: Migrate during low-usage, inform stakeholders, transform data.
5. **Verify**: Check data integrity, update application, monitor performance.
6. **Post-Migration**: Update documentation, notify stakeholders, conduct review.

## Considerations

- **Downtime**: Employ strategies like temporary tables or replication to minimize impact.
- **Data Integrity**: Use careful planning and testing to avoid data loss or corruption.
- **Performance**: Consider new schema's performance implications, focusing on indexing, partitioning, and data types.
