---
share_link: https://share.note.sx/n5twg9de#YqVHXEn251iKPJ+7eNvYthYzWttWrsL/5OhdZb1Ac1c
share_updated: 2025-09-22T12:00:05+03:00
---
## web attacks
### injection  / XSS
- happens due to lack of input validation / sanitization
- can be easily mitigated
### CSRF attacks
- solved with a CSRF token
## Data fetching issues

### under-fetching
- fetching less data than needed
- needing more than 1 endpoint to fetch all data
- causes delays
- may cause n+1 query issues
- may trigger rate limits
- can be handled using a backend-for-frontend

### over fetching
- fetching too much data
- can be also solved via a backend-for-frontend or a graphQL api

### fetching unbounded data
- fetching data that has no limits on size
- causes delays
- can cause performance issues
- can cause UI shifts
- solved using pagination
	- page based
	- cursor based

## Performance 
- better performance is always better
- many things can cause better (or worse performance)

### frontend / mobile

#### UI
- implement Optimistic UI
- implement proper state management to reload as little of the UI as possible
- use server rendering / static generation on the web
- lazy load images
#### Network
- the biggest cause of delays is network requests
- caching API data so we don't hit it so often
- fetch data in parallel and on navigation

### backend
- use efficient queries
- cache frequently accessed data
- always return the least amount of data
- have the database handle database stuff
- have a normalized database schema 
- use the correct database for the task