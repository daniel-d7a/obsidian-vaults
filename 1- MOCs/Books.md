- Get all notes with the books tag
- split to get the book type and make a lvl2 heading
- split to get the book name and make a lvl3 heading
- display all book related notes

```dataviewjs
const pages = dv.pages('#books')
const bookTypes = new Set() 

pages.flatMap(p=>p.file.etags).filter(e=>e.startsWith('#books')).map(e=>e.split('/')[1]).forEach(e=>bookTypes.add(e))

bookTypes.forEach(t=>{
	const bookType = t[0].toUpperCase().concat(t.slice(1))
	dv.header(2, bookType)

	const booksNotes = pages.filter(p=>p.file.tags.includes(`#books/${t}`)).map(p=>p.file.link)

	const bookNames = new Set()
	 



	dv.list(bookNotes)
})

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
