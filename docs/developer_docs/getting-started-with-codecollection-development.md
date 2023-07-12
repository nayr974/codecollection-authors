# Getting Started With CodeCollection Development

CodeCollections represent the bulk of functionality of RunWhen, the code that sits underneath SLIs, SLOs and TaskSets. This section assumes that you have already read the user [Getting Started](../runwhen-platform/getting-started-with-runwhen-platform/starting-from-scratch/) guide and are familiar with creating your own Workspace and configuring an SLX with an SLI CodeBundle, SLO Query and TaskSet CodeBundle.

## The Authors Program

We assume some people reading this are users of the RunWhen platform looking to augment their organization's workspace with their own CodeBundles.  Others reading this may be interested in our CodeCollection authors open source community and RunWhen royalty / revenue share programs.

There are three steps in the authors program:

1. Set up a local development environment and get a 'hello world' CodeCollection up and running on your machine.  At this point, you can begin exploring the various Robot/Python libraries we've built or start building your own.
2. Work with a member of the RunWhen team (over slack) to get it published on the platform so it is built in to images and indexed by RunWhen's search.  At this point, your SLIs and TaskSets can be used by anyone on the platform and your open source contributions can be showcased on the platform.
3. When ready, work with a member of the RunWhen team about moving your repo to the runwhen-contrib github organization, setting up a regression test environment (provided by RunWhen) and a support agreement.  At this point, you start participating in the revenue share / royalties program.

More on the 2023 CodeCollection authors program is here:

<table><thead><tr><th width="401">Resources</th><th> </th></tr></thead><tbody><tr><td>List of SLIs and TaskSets currently being requested by RunWhen users with a who-is-working-on-what</td><td>Github issues-only repo <a href="https://github.com/runwhen-contrib/codecollection-authors/issues">here</a></td></tr><tr><td>Slack workspace to collaborate with RunWhen engineers and other CodeCollection Authors</td><td><p>Slack invite link <a href="https://join.slack.com/t/runwhen/shared_invite/zt-1l7t3tdzl-IzB8gXDsWtHkT8C5nufm2A">here</a>.  </p><p></p><p><em>Feel free to introduce yourself on #general, and please join #codecollection-discussion and #codebundle-updates channels.</em></p></td></tr><tr><td>Talk with our founder</td><td>Book a time to talk <a href="https://cal.mixmax.com/kyle-runwhen/cc-author">here</a></td></tr></tbody></table>

## What is a CodeCollection?

A CodeCollection is simply a git repository that includes CodeBundles (robot files), the python source that supports them, the python imported requirements and metadata about the CodeCollection.

## Development Process

The documentation and tools here assume the following flow:

1. Set up your CodeCollection repository from the template provided to get started quickly.
2. Set up a local development environment using the RunWhen DevTools container and link it to the CodeCollection repository to get all of the same tools we use in development.
3. Iterate through local development, running your SLI or TaskSet on your local machine until the first CodeBundle is in reasonable shape.  Commit it to your CodeCollection repo and create a tagged v0.0.1 release.
4. Work with a member of the RunWhen team to get your CodeCollection repository registered with the platform.  This includes it in a platform CI/CD pipeline and makes it available for users to configure in their SLXs.
5. Build a test Workspace that shows off the initial capabilities of your CodeCollection.  The RunWhen team can help make this available to all platform users, and help promote it.
6. Iterate for your next release.

## Directory Structure

A CodeCollection are laid out in an opinionated directory structure to ensure consistency across the community, a service to your users who may not write CodeBundles but will likely read and audit the source code from many different authors over time.  The docs that follow start with replicating a template repo that we provide.

![Directory Structure](/docs/.assets/dir_struct.png)
*Fresh CodeCollection Repo Example*

## DevTools Container

The DevTools Container approach described in "Configuring Your Development Environment" is intended for use with VSCode running locally in a [VS Code / VS Code Server local container topology](https://code.visualstudio.com/docs/devcontainers/containers).  Other approaches are in development.

## Coding Standards

While coding standards for Python are well documented, coding standards for Robot Framework are not as well understood.  Docs for those are coming shortly.

## Up Next: [Setup Your CodeCollection Repository](./setup-your-codecollection-repository.md)