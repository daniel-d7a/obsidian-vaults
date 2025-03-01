# Multi-tenant e-commerce saas platform

## Landing page

- used to showcase the idea and features.
- has a blog about its story, how it is built, and any new features.
- Built using Astro
- includes: 
	- Home.
	- about.
	- blog.
	- pricing and plans.
	- contact us.
	- showcase.
	- plugins store.

## Store front

- simple e-commerce app
- includes:
	- Home
	- login
	- signup
	- forget password
	- products
	- single product
	- cart
	- checkout
	- account
- UI framework is to be determined [Astro, Next, Nuxt]

> I will have a site builder that has a preview of the
final site in the tenant dashboard, do I need both the 
storefront and the tenant dash to use the same framework?

## Tenant dashboard

- a dashboard that allows the tenant to manage everything.
- built using Next.
- includes:
	- products: a mini cms to manage the products [add, remove, modify, sort, search, change order].
	- products -> [name, desc, price, category, image, quantity (or mark as on demand) [options: name, [value, price]]].
	- products are generic and can have any number of options.

	- site builder: a page to configure the store's theme and style.
	- a section for general settings, and a section for each page in the store front.
	- general settings -> color palette, fonts: {headings, body}, logo, border radius.
	- page section -> placement and varients of componentes.
	- this can have an option for a general theme that applies store wide theme (elegent, default, neo brutalism)

	- statistics: about sales, orders, ...etc.
	- orders: view order details, status (shipped, delivered, canceled)

	- plugins: a system of extensions that add functionality, (e.g. delivery, loyality points, promo codes, discounts, ...etc.)
	- can be used to raise the cost, or implement custom functionality.
	- will have a store page for tenants to view and choose from.
	- each plugin will add some extra settings to this dashboard, (and maybe some functionality to the store front)

	- subscription: view your costs, base cost, plugins, previous transactions, ...etc.

	- roles and permissons: manage the roles and permissons of other members of your organisation.
	- create permissions and assign them to roles, then create or invite users with these roles.
	- example usage could be:
		- members who can only access orders.
		- (future) members with access over one category only.

	- support: a chat where tenants can ask questions, report issues, ask for features, ...etc.
	- this could be a whatsapp number, but needs to be managed by many people.
	
## Admin dashboard

- for managing and viewing the tenants.
- built using Next.
- includes:
	- tenants: show current tenants and stores.
	- statistics: shows data about sales, orders, users, ...etc.
	
	- invoices: an autonomus system for billing and invoicing clients.
	- includes emails about billing, late fees, due dates, ...etc.
	- shows all tenants transactions, plans, bills, due dates, and more...

	- roles and permissions: manages the roles and permissions of other admins
	- can add admins to some tenants only or with specific roles.
	- can add customer support employees.

	- plugins: 	views data and stats about plugins.

	- feature flags: shows the functions and plugins in the system, allows us to quickly turn on or off any feature.





