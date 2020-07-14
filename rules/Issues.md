## Rules for creating an issue.


#### Key points:
1.  If you have no issue for some founded problem, than create it before making changes.
2.  Any issue consists of a title, description, assignee and labels.
3.  Avoid using prefix words in title of issue with type label - "story" such as "Add", "Fix" and etc.
4.  Use the pattern: "ISSUE-{your issue number}/{your-issue-title}" - in branches naming.

### Title
- must be concrete and informative;
- begins with a capital letter;
- continues in small letters.

### Description
- must contains all information about what you want somebody to do;
- can consists of text, pictures, links and other information to make clear the task; 

### Assignees
- should not be empty;
- select from the list.

### Labels
- should not be empty;
- select from the list;
- consist type, priority and status.

#### Types of labels:
- `type:project` - changes in project architecture.
- `type:story` - big changes in logic of project requiring phased implementation.
- `type:task` - a part of story or a task covering several classes.
- `type:subtask` - a part of task. 
- `type:defect` - a bug or mistake in a code.
- `type:blocker` - the most important defect which blocking other features.

#### Priority of labels:
- `priority:critical` - requires immediate execution.
- `Priority:Normal` - there is time to execute.
- `priority:low` - must be completed during the sprint.

#### Statuses of labels:
- `on hold` - can't be completed without another requirements.
- `ready for testing` - requires to check.
- `duplicate` - not a unique.
- `question` - there are some questions.
- `required` additional info - need to get more information.

![alt text](https://i.ibb.co/p2yBp2H/issue.png "Example of an issue")
