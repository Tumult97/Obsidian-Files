
```toc
```

## Problem

The current Credit paper Dashboard is built using an Angular Material TabGroup. This is easy to use. However with all the new sections being added the tabs are now overflowing past the bound of the view and have to be scrolled to find. As this continues the problem will become worse. These tabs will become more and more of an annoyance to find. 

![[Pasted image 20240109123454.png]]

See above. at first glance one cant easily find the newer tabs as they are off screen. SO the user has to find the tab and scroll around. 

Another note is that some of these tabs seem redundant as they have overlapping data that is loaded for each tab. 

## Proposal 1 - Vertical Tabs

> Difficulty: Medium
> Time: Medium
> Impact: Low



## Proposal 2 - Stacked tabs

> Difficulty: Low
> Time: Low
> Impact: Medium



## Proposal 3 - Refactor and Coalesce

> Difficulty: High
> Time: High
> Impact: High

![[Pasted image 20240109124244.png]]

See Above for changes:
___
<p style="color: red">
> 11 Tab have been condensed to 5
</p>

<p style="color: green">
> Due to the removal of tab new ways of filtering need to be added <br/>
> The collapsible section houses 3 filtered than can be used in various different ways to filter data<br/>
> These can be preset and certain one can be hidden and removed for different entitlements
</p>

<p style="color: blue">
> These section now houses a set of pre defined filter chips that will be used <br/>
> These cover the tab that were removed that housed data like location and status
</p>

___
