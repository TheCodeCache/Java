# Code Review – Best Practices : 

Code reviews are performed in order to improve the code quality and the team benefits from the valuable feedback from the peer review(s) and the tech lead(s). For example:

**Sharing Knowledge**  helps the development team in many ways:

- A code review explicitly communicates added/altered/removed functionality to team members who can subsequently build on the work done.
- The committer may use a technique or algorithm that reviewers can learn from. More generally, code reviews help raise the quality bar.
- Reviewers may possess knowledge about programming techniques or the code base that can help improve or consolidate the change; for example, someone else may be concurrently working on a similar feature or fix.
- Positive interaction and communication strengthens social bonds between team members.

## Mandatory list of items to follow for code review/commits:  
1. Comments strictly followed within the source code as needed for the header/inline comments/prior to explaining a function
2. Proper indentation followed for code readability
3. The code functions/works per the description  
4. Follow the commit code guidelines (for e.g. do not remove the whole section of the code and add along with the additional code lines)
5. Post Code review:
   - Comments added in JIRA and the next reviewer is tagged
   - After a pull request is done, the last approver (code reviewer) has to merge right away to resolve any identified issues when reviewing the code 
   - Any technical debt has been added to the log
6. Follow Graceful Degradation design approach that will work in the newest browsers, but also can fall back to deliver the content and render well in older browsers
7. Testing:
   - Before merging the code base, the build tests are passed
8. Follow one naming convention within the source code:
   - Python/Java
   - UI  

**`Consistency`** in a code base makes code easier to read and understand, helps prevent bugs, and facilitates collaboration between regular and migratory developer species.  
**`Legible`** code is more reusable, bug-free, and future-proof.  
**`Accidental errors`** (e.g., typos) as well as **`Structural errors`** (e.g., dead code, logic or algorithm bugs, performance or architecture concerns) are often much easier to spot for critical reviewers with an outside perspective.  

## Commit message guidelines: 
A commit message convention makes it easier to explore a more structured commit history and understand which notable changes have been made between each release of the project.  
Information in commit messages –  
- Describe why a change is being made.
- How does it address the issue?
- What effects does the patch have?
- Do not assume the reviewer understands what the original problem was.
- Do not assume the code is self-evident/self-documenting.
- Read the commit message to see if it hints at improved code structure.
- The first commit line is the most important.
- Describe any limitations of the current code.
- Do not include patch set-specific comments.

**The Type**  

The type is contained within the title and can be one of these types:
- **feat**: a new feature
- **fix**: a bug fix
- **docs**: changes to documentation
- **style**: formatting, missing semi colons, etc; no code change
- **refactor**: refactoring production code
- **test**: adding tests, refactoring test; no production code change
- **chore**: updating build tasks, package manager configs, etc; no production code change

**The Subject**  

Subjects should be no greater than 50 characters, should begin with a capital letter and do not end with a period.  
Use an imperative tone to describe what a commit does, rather than what it did. For example, use **change**; not changed or changes.  

**The Body**  

Not all commits are complex enough to warrant a body, therefore it is optional and only used when a commit requires a bit of explanation and context. Use the body to explain the **what** and **why** of a commit, not the how.  
When writing a body, the blank line between the title and the body is required and you should limit the length of each line to no more than 72 characters.  

**Example Commit** –  
feat:Added AppX support in middleware  
Problem  
AppX needs to be added as a part of deployment in OSS  
Solution  
Added service for AppX Conversation  
Note  
JIRA_NUM-1234  

**Code Review Flow:**  

![image](https://user-images.githubusercontent.com/26399543/153477278-d417cc6b-7420-43ce-9949-6a30afbfb862.png)  

## Java code review checklist: 
**Clean Code:** Code that is easy to understand and easy to change.  

![image](https://user-images.githubusercontent.com/26399543/153477505-89b3ec8f-03a7-4b75-a1b2-eb1bf58f41b9.png)  

**General checks:**  

![image](https://user-images.githubusercontent.com/26399543/153477621-c6d09c2d-bc9b-4b52-ac60-625ae944d12f.png)  

**Performance:**  

![image](https://user-images.githubusercontent.com/26399543/153477730-f56c5224-a270-4685-a678-8def25093f51.png)  

