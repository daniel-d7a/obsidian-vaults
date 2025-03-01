## tenants create schemas with types for thier products, then create products into schemas.

- creating a schema creates a new database table with the specs specified.

- schema table has {id, tenant_id, schema_table_name} that links tenants wih thier schemas.

- each product now also has a {schema_id} property that links it to the correct schema.

- this allows me to have typed properties for products.

- this elemenates the products table, a tenant's products can be obtained from the schemas' tables based on the schemas related to the tenant's id.

## allow users to create typed properties for the product options

- either give them a choice or infere the type based on the value.

- inferring based on the value seems weak.