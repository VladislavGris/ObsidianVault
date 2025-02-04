---
tags:
  - script
info:
  - pack
  - python
---
```python
import json
import sys

def extract_ref_lines(lock_file_path):
    try:
        # Read the lock file
        with open(lock_file_path, 'r') as file:
            lock_data = json.load(file)
        
        ref_lines = []
        
        def find_refs(obj):
            if isinstance(obj, dict):
                for key, value in obj.items():
                    if key == "ref":
                        ref_lines.append(value)
                    elif isinstance(value, (dict, list)):
                        find_refs(value)
            elif isinstance(obj, list):
                for item in obj:
                    find_refs(item)
        
        # Start the search from the root of the JSON data
        find_refs(lock_data)
        
        return ref_lines
    
    except FileNotFoundError:
        print(f"File not found: {lock_file_path}")
        sys.exit(1)
    
    except json.JSONDecodeError:
        print(f"Invalid JSON format in file: {lock_file_path}")
        sys.exit(1)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python script.py <path_to_lock_file>")
        sys.exit(1)
    
    lock_file_path = sys.argv[1]
    ref_lines = extract_ref_lines(lock_file_path)
    
    for line in ref_lines:
        print(line)

```