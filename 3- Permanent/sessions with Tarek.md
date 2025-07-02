[[Eraasoft]]

## Session 1

- was 3 hours
- what he knows about react and the frontend.
- the project he is working on.
- we discussed react in general
	- why react
	- what is react
	- components, jsx, lists, conditional rendering
- hooks
	- use state
	- use reducer
	- use effect

## Session 2

- use context hook
- custom hooks for fetching data
- rules of hooks
- types of state
- better global state management using Zustand
- tan stack query

## Session 3

- routing with react router

- react router provides client side routing, and data loading
- what is client side routing and why we use it?

- basic routing tooling like link, use navigate, use location
- more advanced stuff like loaders, actions, …etc.
- each route has a url and a component.
- we can wrap elements in layouts or bigger elements, or make sub paths
- for sub paths we can use an outlet
- routes without a path create layouts for other components
- index matches the parent url or / if no parent (default route)
- dynamic segments start with a :, it will be parsed and passed as params to the route
- we can make a route segment optional with a ?
- the star is a catch all route
- we use links for navigation
- nav links can show active states
- useNavigate to navigate programatically
- useSearchParams for search params
- useLocation returns an object with info about the current location

- types of routers
- browser router uses the url (the browser's history api)
- hash router uses the fragment portion of the url
- memory router uses internal memory or state for the routes

- for data routes to create nested routes we use the children property
- loaders provide data to route components before they are rendered, using a loader function and useLoaderData
- we can use lazy loading with the lazy prop
- using react query with loaders

- action revalidate the loaders after they are done.
- actions can be called by passing a url to a Form component, or using useSubmit
- forms navigate on submit
- fetchers allow for form submissions without navigation, they have Form and submit
- actions can return data, can be accessed through useActionData or fetcher data

- advanced usage
- navigation blocking using useBlocker, if user is inserting data, …etc
- file based routing (e.g. tanstack router)
## session 4

- i18n
