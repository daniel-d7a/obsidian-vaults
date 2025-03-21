#moc 
```dataviewjs

const inlinks = dv.current().file.inlinks

const inlinkPages = inlinks.map(i=>dv.page(i.path))
const projectsSet = new Set();

inlinkPages.forEach(i => {
	i.file.etags
		.filter(e=>e.startsWith('#project'))
		.forEach(e=>projectsSet.add(e))
})

projectsSet.forEach(source=>{
const projectName = source.split('/')[1]
const displayName = projectName[0].toUpperCase().concat(projectName.slice(1)).replace('_',' ')
	dv.header(2, displayName)


	const data = inlinkPages.filter(i => i.file.etags.includes(source))
	.map(f=>f.file.link)

	dv.list(data)
})

```