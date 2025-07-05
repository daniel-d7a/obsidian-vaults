[[Power I Tech]]
## Questions

- understand the business
- get env file
- get postman working

## Bitwise permission system

- uses a context for permissions
- saves data in local storage
- permissions are module based, we assign 1 to the module index then assign all the bits as user permissions
- 1, 2, 4, 8, 16, 32

## User profile

- settings
- update user data
- reset password

## Users module

- employees tab with all data of employee
	- tabs for totals about employees
	- saving table config to database if not exisit, else get from database
- create new user
- export data as xlsx file
- tabs to manipulate the employees table
- a roles table for the employees
- set user permissions per module and submodule

## Customers

- customers crud table
- customer info and dashboard
- projects crud table

## Sales

- sales employees crud table
- work plans crud table
	- has a full calendar
- visits crud table
- quotation requests crud table
- quotation crud table
- settings
	- little forms with little crud tables

## Fleet

- crud tables, forms,

## Firebase for notifications

## Crud table flow

- define state
- define toggles for tables and modals
- get router, nav bar context, redux state and dispatch
- get permissions
- get api data + save to redux
- get table settings + send to api of not set
- delete is simple api call + toast + refresh data
- handle search
- hadle toggle for features (modals, delete, …etc)
- export is api call
- handle optimize columns ??????
- edit goes to edit page
- add widget data
- render UI
- render modals after UI
- any data that has database categories or types gets fetched and can be displayed in a modal or auto complete

## Crud form

- define state
- define toggles
- define redux
- define react hook form
- get form data from api
- get model by id + set state and form state (if it is an edit)
- handle creating new form data
- get trees ?????????
- submit form data (create / update / delete) + toast
- handle media uplaod using fileUploader
- render UI

## Common components

- table
- table filter
- table pagination
- grids for modals
- triple dot action menu
- file uploader that uses react dropzone, handles multiple file upload and cancelling.
- module widget
- column organizer using drag and drop
- table actions (filter, organize, tree, …etc)
- loading component
- values maps
- data models (propably for intellisense in forms)


tarek.samir.ali@gmail.com
123456789
