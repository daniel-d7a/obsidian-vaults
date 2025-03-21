- what is better? to have a generic product with many options that are unknown in type, or have the tenant create schemas with types for his products?
- A: make the user create a schema for his options on the fly then us it

- what to use for realtime data? server side events for the server and a mutation for the client, or trpc subscriptions?
- A: we can use server side events for somethings like order updates, and trpc subs for others like chat, and inventory updates

- how to save the data related to my pages design and config and different sections in the database?
- A: as json and validate the type in the api level, as this data will not be searched, sorted, or queried against


[[multi-tenant saas e-commerce platform]]