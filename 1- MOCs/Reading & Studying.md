
## articles
```dataview
TABLE WITHOUT ID file.link as Name, file.etags as tags
FROM [[]] AND -"_/_Templates"
SORT file.cday DESC
```
```dataview
TABLE file.link as name, file.tags as tags
FROM [[]] AND -"_/_Templates"
SORT file.cday DESC
GROUP BY filter(file.etags, (tag)=> tag != #sources/articles/tk_dodo )
```
