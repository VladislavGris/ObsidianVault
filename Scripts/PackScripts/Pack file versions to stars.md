---
tags:
  - script
info:
  - pack
  - python
---
```python
import re
import sys

def replace_versions_with_star(content):
    # Regular expression to match "/[...]" where "..." can be anything
    version_pattern = re.compile(r'/(\[[^\]]+\])')
    # Replace only the version part with "/[*]"
    modified_content = version_pattern.sub('/[*]', content)
    return modified_content

def main(file_path):
    try:
        # Read the content of the file
        with open(file_path, 'r') as file:
            content = file.read()
        
        # Replace versions with '/[*]'
        modified_content = replace_versions_with_star(content)
        
        # Write the modified content back to the file
        with open(file_path, 'w') as file:
            file.write(modified_content)
        
        print(f"Versions in {file_path} have been replaced with '/[*]'.")
    
    except Exception as e:
        print(f"An error occurred: {e}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python script.py <path_to_client.yml>")
    else:
        file_path = sys.argv[1]
        main(file_path)
```