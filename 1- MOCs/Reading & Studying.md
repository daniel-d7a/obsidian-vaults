
## articles
```dataview
TABLE WITHOUT ID file.link as Name, file.etags as tags
FROM [[]] AND -"_/_Templates"
SORT file.cday DESC
```
```dataview
TABLE WITHOUT ID
  file.link as "Article",
  filter(file.tags, (t) => startswith(t, "#sources/articles/"))[0] as Source,
  filter(file.etags, (t) => !startswith(t, "#sources/articles/")) as Topics
FROM [[]] 
SORT Source asc
```
```dataviewjs
dv.table(dv.pages(''))
```