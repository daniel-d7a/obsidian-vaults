## tenant

- id
- user_name
- email
- password hash

- one tenant has many products

## product

-id
- name
- description
- image
- base price
- categories
- quantity_in_stock
- on_demand
- tenant_id

- one product has many options
- one product belongs to one tenant
- one product has many categories

## option

-id
- name
- tenant_id

- one option belongs to many products
- one option belongs to one tenant

## product_option

- product_id
- option_id

## category
- id
- name

## product_category
- product_id
- category_id


## store_config

- id

### general settings

- tenant_id
- theme
- heading_font
- body_font
- color_1
- color_2
- color_3
- color_4
- color_5
- border_radius
- logo

### page settings

- home_page_id
- products_page_id
- single_product_page_id
- cart_page_id
- auth_page_id
- chekout_page_id
- user_account_page_id

- one tenant has one store_config.
- one store_config has many pages.
- one page has a name and many sections.
- one section has a varient, and some options.
- section mobile varient is dependent on the desktop varient.

e.g. 
- home page has [Hero, main products, all categories]
- hero has a varient, that varient has some options such as heading, body, button, ...etc.

## page_sections
- id
- page_id
- section_id










