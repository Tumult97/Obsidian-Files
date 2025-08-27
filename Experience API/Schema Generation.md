> We have implemented schema generation in the experience API to allow interfaces the ability to see what model is needed for each Application type and aggregator model type combination


# Overview

The schema generation is done on a [[Application Type]] and [[Aggregator Model Type]] basis. This is because the model here can change because the [[Application Inputs]] change based on the combination. 

# The process

The schema generation is called from an [[Experience Controller]]. 

This then makes a call to the database and gets the template for the [[Application]] which includes the [[Application Inputs]].

It then loops through all the inputs and calls the relevant [[Application in]]