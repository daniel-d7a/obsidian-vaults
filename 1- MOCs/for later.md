#moc

```dataviewjs
const pages = dv.pages('#later')
const books = new Map()

pages.flatMap(p=>p.file.etags).filter(e=>e.startsWith('#later')).map(e=>{
const [, category, subCategory = "unsorted"] = e.split('/');
return {category, subCategory};
 }).forEach(({category, subCategory})=>{
	if(books.has(category)){
		books.set(category, books.get(category).add(subCategory))
	}else{
		books.set(category, (new Set()).add(subCategory))
	}
 })

books.forEach((subCategories, category)=>{
		dv.header(2, category)
		
	subCategories.forEach(b=>{
		b !== "unsorted" && dv.header(3, b[0].toUpperCase().concat(b.slice(1)))
		
		const subCategoryNotes = pages.filter(p=> b !== "unsorted" ? p.file.tags.includes(`#later/${category}/${b}`) : p.file.tags.includes(`#later/${category}`)).map(p=>p.file.link)
		dv.list(subCategoryNotes)
	})
})
```
