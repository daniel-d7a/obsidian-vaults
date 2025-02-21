
## articles
```dataview
TABLE WITHOUT ID file.link as Name, file.etags as tags
FROM [[]] AND -"_/_Templates"
SORT file.cday DESC
```
```dataview
TABLE WITHOUT ID
  file.link as "Article",
  file.etags,
  filter(file.etags, (t) => startswith(t, "sources/articles/")) as Source
FROM [[]] 
GROUP BY filter(file.etags, (t) => startswith(t, "sources/articles/"))[0] as Source
SORT Source asc
```
