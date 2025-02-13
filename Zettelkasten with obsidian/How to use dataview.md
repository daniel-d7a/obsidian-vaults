---
fleeting: true
---

We can query and view the data in 4 ways:
- list
- table
- task
- calendar 

A query must have a type, everything else is optional.

```
List
```

We can search the whole vault or limit the query to a folder, subfolder, or a single file.

```
From <path/to/folder/or/file>
```


We can even search by tag or nested tag.

```
From #<tag_name>
```

We can also use logical operators like AND and OR to combine resources.

```dataview
LIST
FROM "Projects" AND (#project/active OR #project/soon) 
```

With dataview, files now have a lot of metadata available on the global `file` variable, such as:
- creation and modification date and time.
- tags
- lists and tasks
- any properties and inline dataview properties 
- file name, path and extension.
- in and outgoing links

Lists and tasks are not very important to me I guess.

We can add inline DQL to our notes

We can access the current file using `this` or another file using `[[link_to_file]]`



Other things we can use in dataview include:
- sorting with the `SORT` keyword either `ASC` or `DESC`.
- filtering with a `WHERE` clause.
- grouping with a `GROUP BY`.
- using many of the built in functions described in the[[#^docs | docs]].
## references 
- [dataview docs](https://blacksmithgu.github.io/obsidian-dataview/) ^docs
- [Dataview in Obsidian: A Beginner’s Guide (article)](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/)
