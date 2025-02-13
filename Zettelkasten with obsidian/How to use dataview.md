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

Other things we can use in dataview include:
- sorting with the `SORT` keyword.
- filtering with a `WHERE` clause.
- grouping with a `GROUP BY`.
- using many of the built in functions described in the[[#^docs | docs]].
## references 
- [dataview docs](https://blacksmithgu.github.io/obsidian-dataview/) ^docs
- [Dataview in Obsidian: A Beginner’s Guide (article)](https://obsidian.rocks/dataview-in-obsidian-a-beginners-guide/)
