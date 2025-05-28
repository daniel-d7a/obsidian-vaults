## My to-do list for now

- [ ] learn and explain scratch (important)
- [ ] get nice UI for the blog
- [ ] revamp the UI of the blog
- [ ] clean wardrobe
- [x] change YT channel image and banner
- [ ] change Whatsapp image
- [x] send book to htlr
- [ ] go to aunt for lunch
- [x] check the session with menna
- [x] reply to omar
- [ ] check if I have a meeting on friday
- [ ] write a blog post
- [ ] write a video script
- [ ] watch the stuff GPT told you about content and take notes
- [ ] game

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
