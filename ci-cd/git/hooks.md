## CI/CD > GIT > Hooks

[<- To GIT](./index.md)


Git hooks are customizable scripts that Git executes at specific points in the Git workflow. They allow you to automate tasks or enforce policies before or after certain Git commands are executed. Here's an extensive explanation of Git hooks:

1. **Customizable Scripts**: Git hooks are executable scripts written in any programming language or shell script supported by your operating system. These scripts can be tailored to perform various actions or checks in response to Git events.

2. **Event Triggers**: Git provides several predefined events, known as hook points, at which hooks can be triggered. These events include pre-commit, post-commit, pre-push, post-receive, and many others. Each event corresponds to a specific stage in the Git workflow.

3. **Local and Server-Side Hooks**: Git supports both local and server-side hooks. Local hooks run on the developer's machine, affecting only their local repository. Server-side hooks run on the remote repository server and can enforce policies or perform actions for all users interacting with the repository.

4. **Pre-Commit Hooks**: Pre-commit hooks execute before a commit is created. They are useful for performing checks such as linting code, running tests, or ensuring code formatting standards are met. If a pre-commit hook fails (i.e., exits with a non-zero status), the commit is aborted.

5. **Post-Commit Hooks**: Post-commit hooks run after a commit has been successfully created. They are commonly used for tasks such as sending notifications, updating documentation, or triggering continuous integration (CI) pipelines.

6. **Pre-Push Hooks**: Pre-push hooks execute before Git pushes commits to a remote repository. They allow you to perform validations or checks before pushing changes, preventing invalid or problematic commits from being pushed upstream.

7. **Post-Push Hooks**: Post-push hooks run after commits have been successfully pushed to a remote repository. They can be used for tasks such as triggering deployment processes, updating issue trackers, or sending notifications to relevant stakeholders.

8. **Server-Side Hooks**: Server-side hooks execute on the remote repository server when specific actions occur, such as receiving pushed commits or accepting incoming changes. These hooks are useful for enforcing repository-wide policies, access controls, or performing server-specific tasks.

9. **Template Hooks**: Git provides template files for each type of hook, allowing developers to quickly set up and customize hooks for their repositories. These template files are stored in the `.git/hooks` directory of the repository.

10. **Sharing Hooks**: While Git does not provide built-in mechanisms for sharing hooks across multiple repositories, developers can maintain a collection of reusable hooks in a separate directory or repository and symlink them into individual repositories as needed.

11. **Security Considerations**: Git hooks execute arbitrary code and therefore pose security risks if not carefully managed. It's essential to review and understand the contents of hook scripts, especially when using hooks obtained from external sources.

12. **Version Control**: While hook scripts are not version controlled by Git itself, developers can include hook scripts in their repositories and manage them like any other source code files, ensuring consistency and reproducibility across environments.

In summary, Git hooks offer a flexible and powerful mechanism for automating tasks, enforcing policies, and integrating custom behaviors into the Git workflow. By leveraging hooks effectively, developers can streamline their development processes, improve code quality, and enforce project-specific conventions and standards.