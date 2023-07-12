# Setup Your CodeCollection Repository

The RunWhen team has prepared a CodeCollection template so that contributors can get setup faster.

> Note: only public GitHub repos are supported at this time, but support for other version control solutions are on the way.

First we'll want to clone the public template repository.  Feel free to remove the git history of this template by removing the .git directory.

```bash
git clone git@github.com:runwhen-contrib/codecollection-template.git
rm -rf codecollection-template/.git
```

We can now push the template to our own personal CodeCollection repository with no prior history.

> Note: Adjust OWNER and MYCODECOLLECTION to match your repository.  The `git add .` is included for brevity, please be mindful if you've added any files to the directory.

```bash
git init
git add .
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:OWNER/MYCODECOLLECTION.git
git push -u origin main
```

![Directory Structure](/docs/.assets/dir_struct.png)
*Fresh CodeCollection Repo Example*


Congratulations! Your repository is now setup for CodeCollection authoring! We can proceed to setting up our development environment and run some CodeBundles!

## Up Next: [Configure Your Development Environment](./configure-your-development-environment.md)