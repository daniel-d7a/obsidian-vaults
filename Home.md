[[Habit tracker]]

## Today in tasks

**Most important:** work on inertia blog.
**Second most:**
- write the docker video.
- shoot docker video.
- start a series on twitter (the blog vlog) make a post with keynotes and attach the video in the coments
- write a section of the react course (on the phone)
**Low energy tasks:**
- watching stuff.
- German.
- reading.
- Quran.
**Chores:**
- go to aunt
- plan a meeting with hash plus
- clean the kitchen
---

## This week in tasks

**Gaming**
- test survial mode in sniper elite 4 and delete it ➰
- start ghost of tsushima dlc 

**Work**
- finish HTML videos
- start CSS videos
- move videos to drive


 **YouTube**
- docker video 
- typescript video 5 - wide and narrow types
- start the blog vlog

 **React course**
- write 2 sections

 **Deutsch**
- up to video no. 15 

 **Reading**
- (seven languages in seven weeks) finish chapter 3 and ½ chapter 4 

 **Coding**
- finish the comments section of the blog 
- add images

 **House**
- clean balcony 

 **Online yapping**
- tweet everyday

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
