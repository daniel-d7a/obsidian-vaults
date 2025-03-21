#moc 
```dataviewjs

const inlinks = dv.current().file.inlinks

const inlinkPages = inlinks.map(i=>dv.page(i.path))
const sourceSet = new Set();

inlinkPages.forEach(i => {
	i.file.etags
		.filter(e=>e.startsWith('#sources'))
		.forEach(e=>sourceSet.add(e))
})

sourceSet.forEach(source=>{
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
