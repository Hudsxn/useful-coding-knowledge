## CI/CD > GIT > What's GIT

[<- To GIT](./index.md)

#### (Explain Like I'm 5): 
Imagine you have a big box of LEGO blocks. You and your friends are working together to build a huge castle using these blocks. But here's the twist: you all want to work on different parts of the castle at the same time, and you want to make sure nobody messes up the other person's work.

Now, Git is like a magical tool that helps you and your friends work on the castle together without stepping on each other's toes. It keeps track of all the changes everyone makes to the castle and makes sure everything fits together perfectly in the end.

Here's how it works:

**Snapshots**: Git takes snapshots of your castle every time you make a change. So, if you add a new tower or decorate a wall with colorful blocks, Git remembers exactly what it looked like before and after your changes.

**Branches**: Git lets each of your friends work on different parts of the castle without getting in each other's way. It creates separate "branches" for each person, so they can build their towers or add moats without worrying about what someone else is doing.

**Merging**: When someone finishes their part of the castle, Git helps you all put everything together. It "merges" all the changes from different branches into one big castle, making sure everything fits together seamlessly.

**History**: Git keeps a log of all the changes made to the castle over time. So, if you want to see who added the drawbridge or when the courtyard was expanded, Git can tell you exactly what happened and when.

**Collaboration**: Git makes it easy for you and your friends to work together on the castle, even if you're not in the same place. You can share your changes with each other, review them, and decide what to keep or discard.

In simple terms, Git is like a magical LEGO manager that helps you and your friends build a castle together, keeping track of all the changes and making sure everything fits together perfectly in the end.

#### Proper Explaination
Git is a version control system used primarily for managing source code during software development. It tracks changes made to files over time, allowing multiple people to collaborate on projects simultaneously.

Here's how Git works:

1. **Repository**: Git operates within a repository, which is a directory containing all the files and folders for a project. This repository stores the complete history of changes made to the project.

2. **Snapshots**: Instead of storing changes as a series of file differences, Git records snapshots of the entire project at each point in time. This makes it efficient and fast to navigate through different versions of the project.

3. **Branches**: Git allows developers to work on multiple versions of a project simultaneously through branches. Each branch represents an independent line of development, allowing for experimentation and isolation of changes.

4. **Commits**: A commit is a record of changes made to the project at a specific point in time. Each commit has a unique identifier and includes a message describing the changes made.

5. **Merging**: Git facilitates the integration of changes from one branch into another through merging. When merging branches, Git automatically resolves conflicts between changes made to the same file by different contributors.

6. **Remote Repositories**: Git enables collaboration among developers by supporting remote repositories hosted on platforms like GitHub, GitLab, or Bitbucket. Developers can push changes to remote repositories and pull changes from them to synchronize their work with others.

7. **History and Tracking**: Git maintains a complete history of all changes made to the project, allowing developers to track who made specific changes and when. This history provides valuable context and helps troubleshoot issues that arise during development.

8. **Distributed**: Git is a distributed version control system, meaning that each developer has a complete copy of the project's history on their local machine. This decentralization enables developers to work offline and perform version control operations independently.

In summary, Git is a powerful tool for managing collaborative software development projects. It provides robust version control capabilities, allowing developers to track changes, collaborate effectively, and maintain a complete history of their project's evolution.