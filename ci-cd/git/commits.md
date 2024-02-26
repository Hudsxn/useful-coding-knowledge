## CI/CD > GIT > Commits

[<- To GIT](./index.md)

Commits are fundamental units of change within a Git repository. They represent snapshots of the repository's state at a given point in time. When you make changes to files within your Git repository, you stage these changes and then commit them to the repository. Each commit records a specific set of changes along with metadata such as the author's name, email, timestamp, and a unique identifier called a hash.

Here's an extensive breakdown of commits:

1. **Snapshot of Changes**: A commit captures the state of the repository at a particular moment. It includes all the changes made to the files since the last commit.

2. **Atomic Units**: Commits are atomic, meaning they are indivisible units of change. Once committed, they cannot be partially undone. This ensures consistency and integrity within the repository.

3. **Commit Message**: Each commit is accompanied by a commit message, which describes the changes made in that commit. A good commit message is concise yet descriptive, explaining the purpose of the changes.

4. **Unique Identifier**: Every commit has a unique identifier, typically a 40-character hexadecimal string called a SHA-1 hash. This hash is generated based on the commit's contents and metadata and serves as a unique identifier for that commit.

5. **Parent Commits**: Most commits have one or more parent commits, representing the previous state of the repository. This allows Git to track the history of changes and reconstruct the sequence of commits.

6. **Author and Committer**: Each commit records the name and email address of the person who authored the changes (the author) and the person who committed them to the repository (the committer). In many cases, these may be the same person, but in collaborative projects, they can differ.

7. **Timestamp**: Commits also include a timestamp indicating when the commit was made. This helps in understanding the chronological order of commits within the repository's history.

8. **Commit Graph**: Commits form a directed acyclic graph (DAG) within the repository, where each commit points to its parent(s). This graph structure enables Git to efficiently traverse the history of the repository and perform operations such as branching, merging, and rebasing.

9. **Branches and Tags**: Commits are often organized into branches, which are divergent lines of development within the repository. Tags can also be applied to specific commits to mark them as significant milestones, releases, or versions.

10. **Revision History**: The sequence of commits forms the revision history of the repository, allowing users to track changes, review modifications, and understand the evolution of the codebase over time.

11. **Commit Objects**: In Git's internal data structure, commits are represented as commit objects. These objects store the commit's metadata, including the author, committer, timestamp, commit message, and references to the parent commit(s).

12. **Commit Lifecycle**: Commits go through a lifecycle within Git, starting from changes being made to files, staging those changes with `git add`, committing them with `git commit`, and finally pushing them to a remote repository to share with others.

In summary, commits are the building blocks of version control in Git, providing a systematic and efficient way to manage changes to files within a repository while preserving the history and integrity of the codebase. They enable collaboration, tracking of changes, and facilitate the maintenance and evolution of software projects.