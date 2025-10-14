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
- need application type
- Need application specific data(names, uc, step name)

## Questions
- Does the left state depend on the top filter?
	- NO
- What are the squares
	- Ignore them and remove them

## Components Needed
1. ![[Pasted image 20251013123255.png]] LIST ITEM
2. ![[Pasted image 20251013123316.png]] Paginator
3. ![[Pasted image 20251014064243.png]]
   status chip - Generic and common
   leading and training 

## Tasks

1. Create View and routing
2. Add endpoints to fetch data
3. Generate components
4. Create central form to handle state
5. controllers
6. service
7. load

## Icons Needed
- Clear filter
- Chat bubble
- Node link
- right chevron arrow
- left chevron arrow
- check circle
- overdue circle arrow
- warning triangle
- calendar with clock due