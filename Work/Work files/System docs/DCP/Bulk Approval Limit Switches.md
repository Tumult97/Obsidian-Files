```toc
```
--- 


## Workflow Description

### Credit Paper Creation Differences

#### Application Details

When inputting application details and selecting the credit paper type *Bulk Approval Limit Switch* then we add a new field next to it called *Credit Sector*
> ![[Pasted image 20230523093956.png]]


#### Client Management

When on this step in the modal the credit paper can only have an application type of *Single Paper* so the input is pre populated and disabled.
>![[Pasted image 20230523094536.png]]


### Sections

#### Credit Paper Sections
1. Reviewers & Approvers
2. Purpose and Review Dates
3. Collateral
4. Financial Covenants
5. Information Covenants
6. Decision Questionnaire
7. Limit Switches
8. Final Recommendation
9. Upload Files

#### Information Sections
1. Portfolio
2. Ratings
3. Financial (CRS)
4. Product Cart Summary
5. ESG Risk Information
6. Comments
7. Refresh
8. Section Management



---



### Workflow

#### Status: IN PROGRESS

1. Fill out sections and work on Credit Paper
> ![[Pasted image 20230523095105.png]]


2. Fill out Limit Switches logic

![[Limit Switch Modal.canvas]]

3. Progress Credit Paper


## Logic
### Modal Flow

---

![[firefox_Ktml8lLs9Y.gif]]
![[Limit Switch Modal.canvas]]

___

#### Step 1
1. The user is presented with the model with the hierarchy on the left and the empty table section on the right 
	- The user needs to select 1 client and 1 facility
2. Once the user selects a CIF number then the facilities related to that CIF number will be loaded into the table on the right
3. The user then selects the facility they *want to transfer from*
4. This enables the #Next button and allows the user to select step 3 from the stepper at the top

#### Step 2
1. The user is presented with the model with the hierarchy on the left and the empty table section on the right 
	- The user needs to select 1any amount of clients and any amount of facilities
2.  Once the user selects a CIF number then the facilities related to that CIF number will be loaded into the table on the right
3. The user then selects the facility or *facilities they want to transfer to*
4. Once at least 1 facility is selected then the #Next button and the step 3 stepper button is enabled for the user to progress
5. The user can also go #Back to step 1 using the #Back button to make a correction

#### Step 3
1. The user is presented with the modal that has 2 sections
	1. The 1st section is the *from facility* at the top
	2. The 2nd section is the *to facilities* at the bottom
2. The *to facilities* at the bottom are loaded into a list of items that expand when clicked to show more information and have 2 possible inputs
3. The user will input the amount they want to transfer to that facility
4. If the switch is valid/compliant for that facility then the icon on the top left will be a green circle check
5. If the switch is not valid/compliant then the icon top left will be a red warning symbol and a comment input will be visible to add commentary
6. One all the information they need is inputted then they have a few options
	1. #Transfer This will send the information captured to be transferred and save. Once completed the modal will close and load up the save information
	2. #Transer_More This will do the same as #Transfer but will reset the modal once completed instead of closing the modal
	3. #Reset This will reset all info in the modal
	4. #Back to return to step 2


### Admin Screens

> There is one page but it has 2 tabs which has logic as follows


#### Exclusion Items
1. The user here is presented with a section with a table
2. The table shows items that want to be excluded from limit switches
3. The #Add button will open a modal with a dropdown to select more products
4. The actions on the right of the table will allow the user to delete products from the table

#### Product Rules
1. The user is presented with a table that shows the rules added and saved
2. The user can click #Add and will be presented with a modal
	1. The user will see 2 product dropdowns and a toggle switch that says *Is Both Ways*
	2. The user will select product from and product to thats allowed in this rule
		- This is The flow that a product is allowed
	3. The user will then decide if it goes both ways. 
		1. If the toggle is on then the rule will then go both ways instead of just from and to
	4. Then the user clicks #Save and the modal closes and the page is updated
3. The user can also delete saved rules

## Architecture

### App

- Modal has 3 steps in 1 container 
- Step 1 and 2 use an inherited base class since they host very similar logic
- The modal container has 2 selection object that hold the selection data for step 1 and 2 which then feeds into step 3 and renders out
- Step 3 has subscriptions that listen for data changes and rebuild the form every time data is manipulated
- Step 3 collects data together and when transfer is clicked then it takes the data collected form all the inputs and aggregates them into a request


#### Models

##### Limit Switch Selection Model

> This model hold a selection from step 1 or 2.
> The model has 2 lists to hold selections for CIF numbers and facility products.
> There are 2 inputs that determine the max selection count for each of the lists.
> There is also an emitter that emits when facilities are added.

```typescript
export class LimitSwitchSelectionModel {
  selectedCifNumbers: string[];
  selectedFacilities: BulkApprovalLimitSwitchApplicationFacilityProductSource[];
  cifSelectionMax: number;
  facilitySelectionMax: number;
  cifSelectionLimited: boolean;
  facilitySelectionLimited: boolean;

  facilitiesUpdated: EventEmitter<BulkApprovalLimitSwitchApplicationFacilityProductSource> =
    new EventEmitter();

  constructor(
    cifSelectionMax: number = null,
    facilitySelectionMax: number = null
  ) {
    this.selectedCifNumbers = new Array<string>();
    this.selectedFacilities =
      new Array<BulkApprovalLimitSwitchApplicationFacilityProductSource>();
    this.cifSelectionMax = cifSelectionMax;
    this.facilitySelectionMax = facilitySelectionMax;
    this.cifSelectionLimited = !!cifSelectionMax;
    this.facilitySelectionLimited = !!facilitySelectionMax;
  }

  // region [ Accessors ]
  get cifSelectionValid(): boolean {
    return (
      this.selectedCifNumbers.length > 0 &&
      (!this.cifSelectionLimited ||
        this.selectedCifNumbers.length <= this.cifSelectionMax)
    );
  }

  get facilitySelectionValid(): boolean {
    return (
      this.selectedFacilities.length > 0 &&
      (!this.facilitySelectionLimited ||
        this.selectedFacilities.length <= this.facilitySelectionMax)
    );
  }

  get selectionValid(): boolean {
    return this.cifSelectionValid && this.facilitySelectionValid;
  }

  get canAddFacility(): boolean {
    return (
      !this.facilitySelectionLimited ||
      this.facilitySelectionMax === 1 ||
      this.selectedFacilities.length < this.facilitySelectionMax
    );
  }
  get canAddCifNumber(): boolean {
    return (
      !this.cifSelectionLimited ||
      this.cifSelectionMax === 1 ||
      this.selectedCifNumbers.length < this.cifSelectionMax
    );
  }

  // Here for future use
  get selectionMetrics() {
    return this.selectedFacilities.reduce(
      (acc, o) => ((acc[o.cifNumber] = (acc[o.cifNumber] || 0) + 1), acc),
      {}
    );
  }
  // endregion

  // region [ Data methods ]
  addCifNumber(cifNumber: string): void {
    if (this.cifSelectionMax === 1 && this.cifSelectionLimited) {
      this.selectedCifNumbers.pop();
    }
    this.selectedCifNumbers.push(cifNumber);
  }

  removeCifNumber(cifNumber: string): void {
    const index = this.selectedCifNumbers.indexOf(cifNumber, 0);
    if (index > -1) {
      this.selectedCifNumbers.splice(index, 1);
    }
  }

  addFacility(
    facility: BulkApprovalLimitSwitchApplicationFacilityProductSource
  ): void {
    if (this.facilitySelectionMax === 1 || this.facilitySelectionLimited) {
      this.selectedFacilities.pop();
    }
    this.selectedFacilities.push(facility);
    this.facilitiesUpdated.emit(facility);
  }

  removeFacility(
    facility: BulkApprovalLimitSwitchApplicationFacilityProductSource
  ): void {
    const index = this.selectedFacilities.indexOf(facility, 0);
    if (index > -1) {
      this.selectedFacilities.splice(index, 1);
    }
    this.facilitiesUpdated.emit();
  }

  isCifNumberSelected(cifNumber: string): boolean {
    const index = this.selectedCifNumbers.indexOf(cifNumber);
    return index > -1;
  }

  isFacilitySelected(
    facility: BulkApprovalLimitSwitchApplicationFacilityProductSource
  ): boolean {
    const index = this.selectedFacilities.indexOf(facility);
    return index > -1;
  }

  // endregion
}

```

##### Transfer Bulk Approval Limit Switch Request

> This object defines 1 switch instance. The number of instances is defined by the amount of facilities selected in step 2 where the money will be transferred to.
> When transferred the app will send a list of these objects mapped from the data collected in step 1, 2 and 3.

```typescript
export interface TransferBulkApprovalLimitSwitchRequest {
  creditPaperId: number;
  toFacility: BulkApprovalLimitSwitchApplicationFacilityProductSource;
  fromFacility: BulkApprovalLimitSwitchApplicationFacilityProductSource;
  currencyCode: string;
  amount: number;
  comment: string;
}
```

- The to and from facilities are facility object obtained from step 1 and 2
	- The from facility is the same for all instances and is obtained from step 2
	- the to facility changes and is mapped using a for loop and it obtained from the list of facilities obtained in step 2
- The amount is the amount transferred selected in step 3


##### Facility products

```typescript
export interface BulkApprovalLimitSwitchApplicationFacilityProductSource extends ApplicationFacilityProductSource {  
	importType: string;  
	hasWarnings: boolean;  
	isValid: boolean;  
	transferAmount: number;  
}
```

This model extends the facility product source and hold all the facility data to be updated and changed


##### Limit Selection objects to request mapping

![[Steps Data to Request Mapping.canvas]]


#### Buttons






### SVC

### DB
