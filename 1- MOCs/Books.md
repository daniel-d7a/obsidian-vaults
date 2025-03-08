
```dataviewjs
const pages = dv.pages('#books')
const books = new Map()

pages.flatMap(p=>p.file.etags).filter(e=>e.startsWith('#books')).map(e=>{
const [, bookType, bookName] = e.split('/');
return {bookType, bookName};
 }).forEach(({bookType, bookName})=>{
	if(books.has(bookType)){

		books.set(bookType, books.get(bookType).add(bookName))
	}else{
		books.set(bookType, (new Set()).add(bookName))
	}
 })

books.forEach((bookNames, bookType)=>{
		dv.header(2, bookType)
		
	bookNames.forEach(b=>{
		dv.header(3, b[0].toUpperCase().concat(b.slice(1)))
		
		const bookNotes = pages.filter(p=>p.file.tags.includes(`#books/${bookType}/${b}`)).map(p=>p.file.link)
		dv.list(bookNotes)
	})
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
