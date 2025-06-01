## Today's plan

| Time block | Activity                           | Done |
| ---------- | ---------------------------------- | ---- |
| Now        | Finish SE4 mission 2               | ✅    |
| 3:00       | Bath and pray                      | ✅    |
| 3:30       | Find good blog UI                  |      |
| 4:00       | Work on blog UI                    |      |
| 6:00       | Work on react course               |      |
| 7:00       | Go to waled for dinner             |      |
| 8:00       | Write a video script for TS course |      |
| 9:00       | Clean wardrobe                     | ✅    |
| 11:00      | Write a blog post                  |      |

## Major

- [ ] redesign the UI for the Laravel-inertia app
- [ ] Work on my Blog

## Minor

- [ ] write a blog post
- [ ] plan some content
- [ ] work on the react course

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
