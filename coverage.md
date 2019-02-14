% Coverage

# Some basics

* to run the program and gather data

```bash
	coverage run program.py
```
	
* to report on the results

```bash
	coverage report -m
```
	
* to get a HTML listing with links to annotated versions of the source code

```bash
	coverage html
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;then visit `htmlcov/index.html`{.bash}.

* to run the associated unit tests and see the anontated coverage

```bash
	coverage run testClassName.py
	coverage html
```