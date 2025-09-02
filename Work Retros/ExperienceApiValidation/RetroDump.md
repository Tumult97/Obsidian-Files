# Did Well
- OG Planning covered a lot of the feature
- Very robust and used a lot of existing code
- Built in steps to help with journey It helped make the validation for all inputs less complex


# Do Better
- Do plans earlier
- Tracked validators: didn't know how they worked or the reason for them
- Left testing code in without removing
- Left unwanted project file changes and didnt check what caused them

# Lessons
- Learned about Moq `.As()` it helped with the strategy casting definitions
```c#
strategyMock.As<IApplicationInputStrategy>().Setup(x => ...  
strategyMock.As<IExperienceApplicationInputStrategy>().Setup(x => ...
```

- 