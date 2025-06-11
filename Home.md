[[Habit tracker]]

## Today in tasks

**Most important:** work on inertia blog.
**Second most:**
- write a TS video and shoot it.
- write the docker video.
**Low energy tasks:**
- watching stuff. ✅
- German.
- reading. ✅
- Quran. ✅
**Chores:**
- buy a mic splitter or a USB card. ✅
- get the meat out and plan a meal. ✅
- meeting with hash plus. ❌
---

## This week in tasks

**Gaming**
- finish sniper elite 4 and delete it
- start ghost of tsushima dlc

 **YouTube**
- docker video
- typescript video 4 - types and interfaces

 **React course**
- write 2 more sections

 **Deutsch**
- up to video no. 9

 **Reading**
- (seven languages in seven weeks) finish chapter 3 and start chapter 4

 **Coding**
- finish the comments section of the blog

 **House**
- clean bathroom
- clean kitchen
- clean balcony

 **Online yapping**
- tweet 3 times

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
