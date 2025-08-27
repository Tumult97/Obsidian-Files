Each [[Application Inputs]] has their own strategy ([[Strategies]]). This defines their logic based on the [[Application Input Type]]


# Definition

## Interface 
There are two interfaces for the application creation strategies. This allows us to define behavior for the #internal system and the #experience system. 

## Base
The base class implements most of the base behavior for the application creation strategies that will be called 


## Implementation
The implementation has a set structure that the interfaces define. As well if logic needs to be overridden then it will also be done here. 


# Methods

## IsApplicable

This method is what defines and gets called when we need to get the relevant strategy for the specific [[Application Input Type]]. 

## FetchValueAsync

This gets the value from the database

## PersistAsync

This saves the value to the database by either creating or updating the value. 