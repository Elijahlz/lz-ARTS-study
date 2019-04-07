# Top 10 GitHub Best Practices

Staying up-to-date with best practices for all development standards is incredibly tricky. You must be endlessly diligent about your research, testing and verifying across multiple resources. Yikes.

So, we did it for you. You’re welcome 🙂

After scanning thousands of repositories and interviewing hundreds of customers, we created a list of common best practices which we strongly recommend be adopted in every modern software development organization:

## Protect the main branches from direct commits
Anything in the master branch should always be deployable, that’s why you should never commit to the default branches directly and why Gitflow workflow has become the standard. Using branch protection can help you prevent direct commits and of course, everything should be managed via pull requests.

github-branch-protection

## Avoid unrecognized committers
Maybe you are working on a new environment, or you didn’t notice that your Git configuration is incorrect which causes the user to commit code with the wrong email address. Now, their commit is not associated with the right user and makes it nearly impossible to trace back who wrote what.

Make sure that your Git client is configured with the correct email address and linked to your GitHub user. Check your pull requests during code review for unrecognized commits.

unrecognized-commits

## Define CODEOWNERS for each repository
Using the CODEOWNERS feature allows you to define which teams and people are automatically selected as reviewers for the repository. This ability automatically requests a review from the repository owners. Nowadays organizations have dozens if not hundreds of repositories and CODEOWNERS gives the option to define who the repo maintainers are across your organization.

github-codeowners

## Separate secret credentials from source code
When building a Cloud Native app, there are many secrets — account passwords, API keys, private tokens, and SSH keys — that we safeguard. NEVER! commit any secrets into your code. Instead, use environment variables that are injected externally from a secure store.

You can use tools like Vault and AWS Secrets Manager to help with your secret management in production.

There are lots of great tools to identify existing secrets in your code and prevent new ones. For example, Git-secrets can help you to identify passwords in your code. With Git Hooks you can build a pre-commit hook and check every pull request for secrets.

github-secrets-in-code

## Avoid committing dependencies into your project
Pushing dependencies into your remote origin will increase repository size. Remove any projects dependencies included in your repositories and let your package manager download them in each build. if you are afraid of “dependencies availability” you should consider using a binary repository manager solution like Jfrog or Nexus Repository. Check out Git-Sizer by GitHub.

## Separate configuration files from source code
We strongly recommend against committing your local config files to version control. Usually, those are private configuration files which you don’t want to push to remote because they are holding secrets, personal preferences, history or general information which should stay only in your local environment.

## Create a meaningful .gitignore file for your projects
A .gitignore file is a must in each repository to ignore predefined files and directories. It will help you to prevent secret keys, dependencies and many other possible discrepancies in your code. You can choose a relevant template from Gitignore.io.

git-gitignore

## Archive dead repositories
Over time, for various reasons, we find ourself with unmaintained repositories. Maybe you opened a new repository for an ad hoc use case (or you wanted to POC a new tech) or you have some repositories with old and irrelevant code. The problem is the same – those repositories are not actively developed anymore after they served their purpose, so you don’t want to maintain them or other people will rely on/use them. The best practice will always be to archive those repositories which will make them “read-only” to everyone.

github-archive-repo

## Lock package version
Your manifest file holds the information about all of your packages versions to maintain consistent results without breaking your code every time you install your app dependencies. The best practice is to use a manifest lock file to avoid any discrepancies and confirm that you are getting the same packages version each time. The opposite being that you leave your code component version imprecise, are uncertain which version will be installed on the next build and your code may break.

lock-package-version

## Align packages versioning
Although you are using the same package, a different version distribution will make it harder to reuse code and tests in various projects.

If you have a package which is used in multiple projects, try at a minimum to use the same major version across the different repositories.

datree-catalog

What’s next?
All that’s left for you to do is check off each of the aforementioned best practices, on each of your repositories, one by one.

Or, save your sanity and connect with Datree’s GitHub app to scan your repositories and generate your free status report to assess if your repositories align with the listed best practices.
