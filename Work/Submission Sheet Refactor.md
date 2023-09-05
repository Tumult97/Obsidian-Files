
## *Issue*

- There is a weird logic where each tab is independent
- they all have their own save logic that isn't linked
- Save buttons do exist but they are in the tabs themselves
- Difficult to expand


## *Summary*

Locations: 
1. Committee Secretary Dashboard
2. Credit Paper
3. Bulk Sitting?
4. Round Robin?

- Make each tab its own component
- Centralize the save and form logic to the modal as a whole
- No automatic save. 
- Form and saving and loading is handles by the parent modal component
- children become containers for teh logic
- one modal footer with action buttons
- less saving and reloading


## *Diagram*

![[Submission Sheet modal refactor.canvas]]