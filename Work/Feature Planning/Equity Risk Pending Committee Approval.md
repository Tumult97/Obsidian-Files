
```toc
```

## Objective
- Equity risk papers currently do not have a workflow for when they are in a committee sitting
- The goal is to add in this missing workflow step
- Not working since new support workflow refactor
- Current Flow:
  ![[Untitled (1).png]]

> Side objective is to use this an an opportunity to learn how to plan


## Pushers
- We have existing flows to lean on to see existing logic
- We can use the existing logic to see how to add the new approval users. 


## Blockers
- Regression testing
- Committee approval is complicated from memory
- Will most likely need some boy scouting
- May need to add custom action button


## Questions
- should we break up the workflow into 2 different flows for ERAC and STC?
	- Decouples the workflows in case we need to make changes in the future and change the flow/logic
	- More explicit code
- Should we combine them?
	- Simpler
	- less duplication of code currently
- Do we need to add an action? maybe 2
	- One to send for approval 
	- One for approval from the approval users
- Can equity risk be part of a bulk sitting?
	- If yes is this accounted for?


## Technical

- No equity risk explicit strategy
- Existing Action => ` SendForCommitteeApprovalCreditPaperAction.cs `
	- Side not refactor ` setDisabledState ` to reduce Cognitive complexity
- There is some logic in ` ApplicationService.cs ` line 176
	- Sets target status based on approvals and if its a committee sitting
	- Method Name: ` GetStatusFromUserApprovals `
	- Used in:
		- #Limit_Switch ` ApproveStatusUpdateStrategy.cs ` line 165 (Side note: Auth header here not used)
		- #Single_Paper ` ApprovedPaperStatusUpdateStrategy ` line 317: method => 
		  ` GetNewApplicationStatusFromUserApprovals `
			- Called in ` UpdateStatusAsync `
- ` GenerateUpdateStatusRequestsForSlotAllocatedPapersPendingLock ` => This also references the status and what does this do?


## Tasks

1. Make new Credit Paper Action
2. Make new strategy for sending for Pending Committee Approval
	1. Possible 2 (see [[#Questions]])
		1. ERAC
		2. STC
3. Make new action for approving from approval users
4. Make Strategy for handling approval and eventual status update
	-  Possible 2 Different strategies (see [[#Questions]])
	1. ERAC
		1. Chairperson
		2. Core Voting Member
		3. Core Voting Member
		4. Core Voting Member
	2. STC
		1. Normal List of users

> The Strategies will be linked to equity risk


## Basic Layout

![[Equity Risk Committee Approval.canvas]]
![[Equity Risk Committee Approval.png]]