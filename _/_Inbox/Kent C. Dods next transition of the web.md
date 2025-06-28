#sources/articles/kent_c_dods

[[Readings & Studying]]

[Article link](https://www.epicweb.dev/the-webs-next-transition)

## Introduction

The web has seen many trends in its architecture, most notable:

- MPA
- MPA + some JS
- SPA

Each trend has its trade-offs, and each trend have also had enough pain points to motivate the move to the next trend.

We will try to discuss each in terms of 6 points.

- rendering
- routing
- feedback to user interactions
- persistence
- data fetching
- data mutation

## MPA

This was used in the early days of the web as it was the only architecture possible

Here everything but the UI feedback lived on the server and was handled by the browser

The browser's role was to only issue requests to the server and show a loading feedback, the the server would route the request, get the data from persistence, render the UI, then send the result back, or in the case mutations, route, process the mutation, update persistence, then return a redirect response to the browser to redirect to the get route explained above.

### pros
- very simple and predictable.
### cons
- full page refresh makes many things hard or out right impossible
    - Focus management
    - animated view transitions
    - simple actions that don't really need a full refresh (liking a tweet)
## PEMPA
Progressivly enhanced multi page application 

