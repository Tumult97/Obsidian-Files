
```toc
```

## Ticket

> [\[CRICRT-8775\] DCP: Approval Users for ERAC workflow - Standard Bank JIRA](https://aws-tools.standardbank.co.za/jira/browse/CRICRT-8775)


## Requirement

- The approval users are
    - Chairperson
    - Core Voting Member 1
    - Core Voting Member 2
    - Core Voting Member 3
    - LE
    - DA
- If any of these members are the same (eg: DA == LE == Core Voting Member 1), then only one approval is needed for that specific person


## Existing Code

- ` ApplicationUserTypeConstants.cs `
  > Has existing list of approval users
```c#
public static List<string> TypesRequiringDecision => new()  
{  
    GroupCreditManager,  
    DelegateAuthority,  
    LegalEntity,  
    Da4VotingMember,  
    GlobalMarketManager,  
    GlobalHeadOfMarketRisk,  
    CibHeadOfCountryRisk,  
    HeadOfCreditInCountry,  
    RiskChair,  
    RiskSponsor,  
    CountryRiskApprover,  
    ProductLimitSupporter,  
    BusinessExecutiveVotingMember,  
    CoreVotingMember,  
    Chairperson  
};
```


- This is used to distinguish approval users


## Proposed solution

- Split into STC and ERAC strategies for committee approval
	- Need to add Way to check if paper is a committee sitting paper in the is applicable
	- Possible override to the Inapplicable
- Possibly split into 3 lists
	- Base list
	- STC approval users
	- ERAC approval users
	- Add getters to combine lists where necessary

[[ERAC Users Canvas.canvas|ERAC Users Canvas]]
![[ERAC Users Canvas.png]]