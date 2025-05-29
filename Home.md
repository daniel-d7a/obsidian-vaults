## My to-do list for now

- [ ] 
- [ ] work on react course
- [ ] get nice UI for the blog
- [ ] revamp the UI of the blog
- [ ] clean wardrobe
- [ ] change Whatsapp image
- [ ] go to aunt for lunch
- [ ] call eraasoft to check for a friday meeting and discuss pay
- [ ] write a blog post
- [ ] write a video script

## Major

- [ ] work on react course
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
