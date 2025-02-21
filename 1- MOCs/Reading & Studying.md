## Articles

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

const inlinks = dv.current().file.inlinks
dv.list(inlinks)


const inlinkPages = inlinks.map(i=>dv.page(i.path))
const sourceSet = new Set();

inlinkPages.forEach(i => {
	i.file.etags
		.filter(e=>e.startsWith('#sources'))
		.forEach(e=>sourceSet.add(e))
})

dv.list(sourceSet)

sourceSet.forEach(source=>{
	dv.header(2, source.split('/')[0].slice(1))

	// get data with {source}
	// group into {topics}
	// display into a table sorted by {topic}

	const data = inlinkPages.filter(i => i.file.etags.includes(source))

	const topicGroups = data.array().reduce((acc,curr)=>{
		const tagsWithoutSource = curr.file.etags.filter(e=>e !== source)

		if(acc[tagsWithoutSource]){
			acc[tagsWithoutSource].push(curr.file.link)
		}else{
			acc[tagsWithoutSource] = [curr.file.link]
		}
		return acc;
	, {})


	dv.table(topicGroups)

	dv.table(['Name', 'Topic'])
})

```

```
const inlinks = dv.current().file.inlinks

dv.table(['article', 'source', 'topics'], inlinks)

dv.table(
	['article', 'source', 'topics'], 
	dv.current().file.inlinks
	.map(
		p=>[
			p.file.name,
			p.file.etags.filter(t=>t.startsWith('#sources/articles/')),
			p.file.etags.filter(t=>!t.startsWith('#sources/articles/'))
		]
	)
)
```
