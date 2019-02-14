% Syntax highlighting in markdown


# Python

```python
import filecmp

# check the working directory
wd = os.getcwd()
print("Working directory: ", wd)
```

# JavaScript

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

# Ruby

```ruby
require 'redcarpet'
markdown = Redcarpet.new("Hello World!")
puts markdown.to_html
```