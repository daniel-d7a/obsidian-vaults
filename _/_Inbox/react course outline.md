---
share_link: https://share.note.sx/4fi3zrcu#nJzugFRuAdvUeHL5x1tx46YaADidMwSsB92TIKVnNCg
share_updated: 2025-03-20T17:38:10+02:00
---

[[Eraasoft]] 
#project/react

## ايه و ليه و ازاي ؟

- ايه هي react ؟
- ليه نستخدم react ؟
- يعني ايه SPA ؟
- ال SPA و ال SSR و ال SSG.
- مقارنة ما بين react وباقي ال frameworks
- ازاي نبدأ مشروع react ؟

## نود و npm

- تحميل node.js
- ما هو npm و ما هي البدائل له (yarn, pnpm)
- ما هو package.json و package-lock.json
- اهم اجزاء ال package.json (ال dependencies و ال scripts )

## تجهيز بيئة العمل

- يعني ايه bundler و اشهر الامثلة عليهم
- ليه بنستخدم bundler ؟
- يعني ايه transpiler و ليه بنحتاجه و اشهر مثال عليه (babel)
- تجهيز vite
- تجهيز git
- تجهيز prettier و ال linter

## مراجعة سريعة على بعض اجزاء ال javascript

- arrays and array methods
- promises
- short circuiting
- ternary operator
- mutability and immutability
- JS modules and import/export syntax

## اساسيات react

- JSX
- components
- props
- state
- component life cycle
- rendering lists
- conditional rendering
- code side effects

## React hooks

- useState
- useReducer
- useEffect
- useRef
- useContext
- useMemo
- useCallback
- شوية hooks تانية مش مهمة قوي (useSyncExternalStore, useId, useImparativeHandle, و غيرهم)
- rules of hooks
- custom hooks and common mistakes

## Typescript

- مراجعة سريعة على typescript
	- basic types
	- function types
	- object types
	- unions and intersections
	- generics
- how to setup react with typescript
- props
- children
- events
- hooks
- context
- generic components
- لو في حاجة زيادة احتجناها ممكن نضيفها هنا بعدين

## Routing

- يعني ايه client side routing (و ده مش حاجة مميزة لل spa بس)
- الفرق ما بين ال client routing و ال server routing
- تجهيز react router
- التنقل من صفحة للتانية باكتر من طريقة
- التعامل مع ال query params و ال route params
- nested routes
- layouts
- catch all routes
- authentication and protected routes
- navigation patterns (blocking navigation, replacing navigation history, redirection after navigation)
- استخدام tanstack router كبديل ل react router

## State management

- component state vs global state with examples
- ايه هو ال context api و ليه هو مش حل لل global state
- اشهر الحلول لل global state management
	- redux
	- zustand
	- jotai
- استخدام ال url ك global state

## Styling

- ايه الخيارات المتاحة ليك ؟
	- regular CSS
	- CSS modules
	- SASS
	- CSS-in-JS (styled-components, vanilla extract, emotion, …etc)
	- tailwind
	- UI libraries (bootstrap, bulma)
	- component libraries (shadcn, material, chakra)
	- headless libraries (headless ui, radix ui)
- امتى استعمل ايه ؟
- ازاي تعمل design system

## Forms

- controlled vs uncontrolled components
- basic form handling and validation (without libraries)
- using a validation library (zod, yup)
- using a form management library (react-hook-form)
- advanced form patterns
	- image and file upload,
	- drag and drop file upload
	- variable number of inputs
	- debounce and throttle
	- multi step forms

## Data fetching

- how to fetch data in react
- fetch api vs axios vs ky
- error handling and error boundaries
- loading state
- race conditions
- throttle and debounce
- managing server state with tanstack query
- infinite scrolling
- pagination
- other data fetcing libraries (apollo, trpc, …etc)
- using websockets for realtime data
- authentication

### Testing React Applications

- Testing philosophy and approaches
- vitest fundamentals
- React Testing Library
- Component testing strategies
- mocking dependencies
- mocking the api using msw
- Testing hooks and custom hooks
- Integration tests
- E2E testing with Playwright

## Organization and best practices

- folder structure
	- atomic design
	- feature based
- env folder and configuration

## Modern react features

- server side rendering
- react server components
- server actions
- new hooks
	- use
	- useFormAction
	- useFormState
- suspense
- streaming data and html
- react forget - the react compiler

## Performance

- memoization with react.memo
- using useCallback and useMemo
- import later
	- on interaction
	- on visibility
- lazy loading
- route based code splitting
- preloading
- prefetching
- list virtualization

## Some react patterns

- prop drilling and how to avoid it
- higher order components
- render props
- component composition
- compound components
- prop getters

## Advanced topics

- how react works (reconciliation and v-dom)
- intro to Next.js
	- دي هتكون مجموعة من الفيديوهات بتشرح فكرة ال framework و الفرق عن react و هيكون عليها تطبيق fullstack عملي
- نظرة على react native
- نظرة على vue.js
- where to go next ?

## Extra topics

- using storybook
- react in other contexts (mobile, desktop, email, pdf, cli, …etc)
- animation with framer motion
- i18n
- a11y

---

## Projects

### Basic

- simple notes app / task manager with local storage
- simple form
- weather app / github user finder
- portfolio website

### Intermediate

- movie watchlist app
- recipe finder app
- quiz app

### Advanced

- e-commerce website
- multi-user blog platform
- chat app
- personal finance app
- social media app
