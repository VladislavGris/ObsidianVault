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

def read_dependencies(file_path):
    """Read dependencies from the first file and extract major versions."""
    dependencies = {}
    with open(file_path, 'r') as file:
        for line in file:
            line = line.strip()
            if line:
                parts = line.split('/')
                if len(parts) == 2:
                    name, version = parts
                    major_version = version.split('.')[0]
                    dependencies[name] = major_version
    return dependencies

def replace_all_versions(file_path, dependencies):
    """Replace all [*] placeholders with [~=major] in the second file."""
    with open(file_path, 'r') as file:
        content = file.read()

    # Replace all [*] placeholders with [~=major] for matching dependencies
    for name, major_version in dependencies.items():
        pattern = re.compile(re.escape(name) + r'/\[\*\]')
        replacement = f"{name}/[~={major_version}]"
        content = pattern.sub(replacement, content)

    # Write the updated content back to the file
    with open(file_path, 'w') as file:
        file.write(content)

def main():
    if len(sys.argv) != 3:
        print("Usage: python script.py <dependencies_file> <target_file>")
        sys.exit(1)

    dependencies_file = sys.argv[1]
    target_file = sys.argv[2]

    # Read dependencies and replace versions
    dependencies = read_dependencies(dependencies_file)
    replace_all_versions(target_file, dependencies)

    print(f"All [*] placeholders in '{target_file}' have been updated with appropriate versions.")

if __name__ == "__main__":
    main()
```