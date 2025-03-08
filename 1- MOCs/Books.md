- Get all notes with the books tag
- split to get the book type and make a lvl2 heading
- split to get the book name and make a lvl3 heading
- display all book related notes

<<<<<<< HEAD
```dataviewjs
const pages = dv.pages('#books')



const bookTypes = new Set() 

dv.list(bookTypes)
=======


```dataviewjs
const pages = dv.pages('#books')

const bookTypes = new Set() 

dv.list(pages)
>>>>>>> 0a7e537 (manual commit)
```

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