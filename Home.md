## Today's plan ✅

| Time block | Activity                                   | Done |
| ---------- | ------------------------------------------ | ---- |
| Now        | clean room                                 | ✅    |
| 3:00       | work on blog UI (make docker work)         |      |
| 12:00      | game                                       | ✅    |
| 7:30 pm    | go to aunt for dinner                      | ✅    |
|            | spend an hour (read, Quran, )              |      |
|            | start Dutch course                         |      |
|            | write the [[useSyncExternalStore article]] |      |

## Major

- [ ] redesign the UI for the Laravel-inertia app
- [ ] Work on my Blog

## Minor

- [ ] write a blog post
- [ ] plan some content
- [ ] work on the react course

## All things I want to do daily

- [ ] write code
- [ ] write non-code
- [ ] read
- [ ] game
- [ ] Quran
- [ ] clean physical space
- [ ] clean digital space
- [ ] tweet
- [ ] learning Dutch

---

## What topics do I have?

```dataview
TABLE  WITHOUT ID file.link as "Note", length(file.inlinks) as "connections"
FROM "1- MOCs"
SORT length(file.inlinks) DESC
```

---

## How many notes do I have? `$=dv.pages("").length`

## How many notes need my attention?

### Incomplete: `$=dv.pages('"_/_Inbox"').length`

### Unorganized: `$=dv.pages('"2Fleeting"').length`

---

## Some random topics

```dataview
TABLE WITHOUT ID file.link as "Note", file.mday as "Last Modified"
FROM ""
SORT hash(dateformat(date(today), "YYYY-MM-DD HH:mm"), file.name)
LIMIT 5
```
