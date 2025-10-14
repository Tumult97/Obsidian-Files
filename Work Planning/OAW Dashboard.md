
![[Pasted image 20251013122106.png]]

## Task View (Left Panel)
- These are loaded for the per task basis
	- Load up from book mark
- Completed
	- Loaded from other table

## Filters
- Have 1 form that loads up
	- Have 1 set initial state
	- load up tasks on page load
	- have filter debounce to prevent very fast request
	- Have request cancelling on filter updates ([[Filters]])
- Bonus task: have 1 service that holds form state and loads that up when returning back. 
- Stats needed for left panel. Have endpoint to fetch those stats
- Add debounce on search filed to prevent too many request being made on key press
- clear filter needs to clear the top filter selection. 
- of top filter is changed then reset pagination to prevent confusion
- [[Filter request cancellation]]

## Needs doing(Not obvious)
- need due date and all relevant data for task display


## Questions
- Does the left state depend on the top filter?

## Tasks

1. Create View and routing
2. Add endpoints to fetch data
3. Generate components
	1. ![[Pasted image 20251013123255.png]] LIST ITEM
	2. ![[Pasted image 20251013123316.png]] Paginator
4. Create central form to handle state
5. controllers
6. service
7. load
 