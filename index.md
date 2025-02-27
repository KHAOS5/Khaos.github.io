---
layout: default
---
[Link to another page](./another-page.html).

There should be whitespace between paragraphs.

There should be whitespace between paragraphs. We recommend including a README, or a file with information about your project.

# Header 1

This is a normal paragraph following a header. GitHub is a code hosting platform for version control and collaboration. It lets you and others work together on projects from anywhere.

## Header 2

> This is a blockquote following a header.
>
> When something is important enough, you do it even if the odds are not in your favor.

### Header 3

```python
# This is a Python code to sort and match hashes from dumping the SAM file.
# This code will look at the raw extracted hashes with usernames and compare then to the cracked hash with the clear text password
# It will then sort then to display the username, hash and the cracked password

#!/bin/python3

# Check if correct arguments are provided
if len(sys.argv) != 4:
    print("Usage: python3 script.py <ntlm_dump_file> <cracked_password_file> <output_file>")
    sys.exit(1)

# File names from command line arguments
ntlm_dump_file = sys.argv[1]
cracked_password_file = sys.argv[2]
output_file = sys.argv[3]

# Read the cracked passwords into a dictionary
cracked_passwords = {}

try:
    with open(cracked_password_file, 'r') as cracked_file:
        for line in cracked_file:
            parts = line.strip().split(":")
            if len(parts) == 2:
                hash, password = parts
                cracked_passwords[hash] = password
except FileNotFoundError:
    print(f"Error: Cracked password file '{cracked_password_file}' not found!")
    sys.exit(1)

# Process the NTLM dump file and match hashes with cracked passwords
try:
    with open(ntlm_dump_file, 'r') as ntlm_file, open(output_file, 'w') as output:
        for line in ntlm_file:
            parts = line.strip().split(":")
            if len(parts) < 2:
                continue  # Skip empty lines or malformed entries

            username = parts[0]
            ntlm_hash = parts[1].strip(":")

            # If there is no username or hash, skip this entry
            if not username or not ntlm_hash:
                continue

            # Remove everything before and including the first backslash (domain)
            username = username.split("\\")[-1]

            # Check if the hash is in the cracked_passwords dictionary
            if ntlm_hash in cracked_passwords:
                password = cracked_passwords[ntlm_hash]
                output.write(f"User: {username}, NTLM Hash: {ntlm_hash}, Cracked Password: {password}\n")
            else:
                print(f"No cracked password found for NTLM Hash: {ntlm_hash}")

    print(f"Matching results saved to {output_file}")

except FileNotFoundError:
    print(f"Error: NTLM dump file '{ntlm_dump_file}' not found!")
    sys.exit(1)
```

```ruby
# Ruby code with syntax highlighting
GitHubPages::Dependencies.gems.each do |gem, version|
  s.add_dependency(gem, "= #{version}")
end
```

#### Header 4

*   This is an unordered list following a header.
*   This is an unordered list following a header.
*   This is an unordered list following a header.

##### Header 5

1.  This is an ordered list following a header.
2.  This is an ordered list following a header.
3.  This is an ordered list following a header.

###### Header 6

| head1        | head two          | three |
|:-------------|:------------------|:------|
| ok           | good swedish fish | nice  |
| out of stock | good and plenty   | nice  |
| ok           | good `oreos`      | hmm   |
| ok           | good `zoute` drop | yumm  |

### There's a horizontal rule below this.

* * *

### Here is an unordered list:

*   Item foo
*   Item bar
*   Item baz
*   Item zip

### And an ordered list:

1.  Item one
1.  Item two
1.  Item three
1.  Item four

### And a nested list:

- level 1 item
  - level 2 item
  - level 2 item
    - level 3 item
    - level 3 item
- level 1 item
  - level 2 item
  - level 2 item
  - level 2 item
- level 1 item
  - level 2 item
  - level 2 item
- level 1 item

### Small image

![Octocat](https://github.githubassets.com/images/icons/emoji/octocat.png)

### Large image

![Branching](https://guides.github.com/activities/hello-world/branching.png)


### Definition lists can be used with HTML syntax.

<dl>
<dt>Name</dt>
<dd>Godzilla</dd>
<dt>Born</dt>
<dd>1952</dd>
<dt>Birthplace</dt>
<dd>Japan</dd>
<dt>Color</dt>
<dd>Green</dd>
</dl>

```
Long, single-line code blocks should not wrap. They should horizontally scroll if they are too long. This line should be long enough to demonstrate this.
```

```
The final element.
```
