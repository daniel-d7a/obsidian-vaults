
```dataviewjs

const inlinks = dv.current().file.inlinks

const inlinkPages = inlinks.map(i=>dv.page(i.path))
const projectsSet = new Set();

inlinkPages.forEach(i => {
	i.file.etags
		.filter(e=>e.startsWith('#eraasoft'))
		.map(e=>e.split('/')[1])
		.forEach(e=>projectsSet.add(e))
})

projectsSet.forEach(source=>{
const sourceName = source.split('/')[1]
	dv.header(2, sourceName[0].toUpperCase().concat(sourceName.slice(1)))

	// get data with {source}
	// group into {topics}
	// display into a table sorted by {topic}

	const data = inlinkPages.filter(i => i.file.etags.includes(source))

	const topicGroups = data.array().reduce((acc,curr)=>{
		const tagsWithoutSource = curr.file.etags.filter(e=>e !== source)

		tagsWithoutSource.forEach(t=>{
			if(acc[t]){
				acc[t].push(curr.file.link)
			}else{
			acc[t] = [curr.file.link]
			}
		})


		return acc;
		}, {})

	dv.table(['Topic', 'Name'], Object.entries(topicGroups).map(([key, value])=>[key, value]))
})

```

```

```