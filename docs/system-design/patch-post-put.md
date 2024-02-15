# PATCH vs POST and PUT

Quick summary highlighting the differences between `PATCH`, `POST`, and `PUT`:

- **POST**:

  - Used to create a new resource.
  - Sends data to the server to create a new entry in a collection.
  - Does not require the full resource representation.

- **PUT**:

  - Used to update/replace an existing resource in its entirety.
  - Requires the client to send the complete updated entity, including both modified and unmodified fields.
  - Idempotent: Repeated requests with the same data result in the same state of the resource.

- **PATCH**:
  - Used for partial updates to an existing resource.
  - Only the fields that are being changed need to be sent.
  - More efficient for small updates, as it reduces data transfer and processing.
  - Ideal for updating a subset of a resource's attributes, such as metadata or tags, without affecting the rest of the resource.

In summary, `PATCH` is chosen for efficiency and specificity when updating parts of a resource, `POST` for creating new resources, and `PUT` for complete replacements of existing resources.

Check [this](./add-json-into-sql-database) for an example of using PATCH when dealing with partial updates to existing database.
