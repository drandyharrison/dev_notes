% git tips

# Create a repo from an existing project

Creates a local repo:

* go to the directory containing the project.

```bash
	$ git init .
	$ git add [relevant files]
	$ touch .gitignore
	$ git add .gitignore
	$ git commit . -m "commit message"
```

To push the local repo to GitHub:

* create a new repo in GutHub but don't initialise it

	* in the upper-right corner of any page click + then click **new repository**;
	* in the owner drop-down, select the account on which you wish to create the repository;
	* give the repository the same name as the local repo - and add an optional description;
	* don't choose any of the options to pre-populate the repository; and
	* click **create repository**.

* at the command prompt (in the directory where the local repo is located):

```bash
	$ git remote add origin https://github.com/drandyharrison/[repo_name].git
	$ git push -u origin master
```

# Remove a file from a github repo

```bash
	$ git rm [filename]
	$ git commit -m "remove [filename]"
	$ git push origin master
```

# To temporarily ignore files

To temporarily ignore changes in a certain file, run:

```bash
	$ git update-index --assume-unchanged <file>
```

Then when you want to track changes again:

```bash
	$ git update-index --no-assume-unchanged <file>
```

There’s quite a few caveats that come into play with this. If you git add the file directly, it will be added to the index. Merging a commit with this flag on will cause the merge to fail gracefully so you can handle it manually.

