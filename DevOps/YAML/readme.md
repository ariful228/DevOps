# YAML Overview

## What is YAML?
`YAML` (YAML Ain't Markup Language) is a **human-readable** data serialization standard used primarily in configuration files and data exchange. It is often used in DevOps, infrastructure as code, and various configuration management systems like **Kubernetes** and **Docker**.

---

## Key Features (50 Points):

### **General Features:**
1. **Human-readable**: Easy to read and write for humans.
2. **Data Serialization**: Converts data structures into a format that can be stored or transmitted.
3. **Whitespace Sensitive**: Indentation is used to define structure.
4. **Supports Comments**: Comments can be added using `#`.
5. **File Extension**: Typically uses `.yaml` or `.yml` extensions.
6. **Compact**: Offers a more compact format compared to XML and JSON.
7. **Language Agnostic**: YAML can be used in any language environment.
8. **No Quotes Required**: Strings don’t need to be quoted unless necessary.
9. **Flexible**: Can represent complex structures (lists, mappings, nested objects).

### **Basic Syntax:**
10. **Key-Value Pair**: Data is stored in `key: value` format.
11. **Indentation**: Hierarchical structure is represented through indentation (spaces only, no tabs).
12. **Lists**: Lists can be represented using a dash `-`.
13. **Multiple Documents**: YAML can store multiple documents in one file, separated by `---`.
14. **Anchors & Aliases**: Reuse parts of a file with anchors (`&`) and aliases (`*`).
15. **Folded Block**: Use `>` to merge newlines into spaces in multi-line strings.
16. **Literal Block**: Use `|` to preserve newlines in multi-line strings.
17. **Explicit Data Types**: Data types can be explicitly defined using `!!type`.
18. **Null Values**: Represent null values using `null`, `~`, or leave it blank.
19. **Booleans**: Booleans can be represented as `true/false`, `yes/no`, or `on/off`.

### **Advanced Features:**
20. **Flow Style**: Data can be represented inline similar to JSON (`{ key: value }`).
21. **Block Style**: YAML uses block-style by default, utilizing indentation.
22. **Mappings**: Allows mapping keys to values, similar to JSON objects.
23. **Sequences**: Allows listing values, similar to arrays in other formats.
24. **References**: Use references to avoid repetition of data structures.
25. **Tags**: Use tags to assign specific data types to values.
26. **Date & Time**: Date/time values can be represented directly.
27. **Binary Data**: Can encode binary data using Base64.
28. **Multi-document**: Store multiple YAML documents in the same file using `---`.
29. **Cross-platform**: Works on various systems and environments.

### **Data Structures:**
30. **Scalars**: Simple values like numbers, strings, booleans.
31. **Mappings**: Define mappings of key-value pairs, equivalent to dictionaries or objects.
32. **Nested Mappings**: Supports complex, nested data structures.
33. **Sequences**: Ordered lists of items, akin to arrays or lists.
34. **Maps of Maps**: YAML can represent mappings within mappings.
35. **Maps of Sequences**: Mappings can contain lists (sequences).
36. **Sequences of Mappings**: Lists can contain key-value pairs (maps).

### **Compatibility:**
37. **JSON Compatible**: YAML is a strict superset of JSON.
38. **Language Support**: Many languages (Python, Java, Ruby) have libraries for YAML.
39. **Used in Infrastructure Tools**: Tools like **Ansible**, **Docker Compose**, and **Kubernetes** use YAML.
40. **Serialization Libraries**: Supported in serialization libraries for converting data into and out of YAML.
41. **API Configurations**: Commonly used in API services for defining requests and configurations.
42. **Configuration Management**: Popular choice for storing application and service configurations.

### **Security & Usability:**
43. **No Execution**: YAML files do not execute code, making them safer to use.
44. **Schema Validation**: Many YAML parsers support schema validation.
45. **Data Interoperability**: Ensures easy data exchange between systems.
46. **Strongly Typed**: YAML allows you to explicitly define data types for accuracy.
47. **Minimal Syntax**: Avoids unnecessary characters, making files cleaner and smaller.
48. **Machine-friendly**: Despite being human-readable, YAML can also be parsed easily by machines.
49. **Safe Mode Parsing**: Many parsers offer safe parsing mode to avoid code injection risks.
50. **Custom Tags**: Allows the use of custom tags to create user-defined data types.

---

## Basic Syntax Rules:

1. **Key-Value Pair**:  
   Defined by `key: value`.

2. **Indentation**:  
   Structure is defined by spaces, not tabs.

3. **Lists**:  
   Defined by dashes `-`.

4. **Comments**:  
   Use `#` for adding comments.

---

## YAML Example:
```yaml
# Example Kubernetes Service configuration
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: MyApp
  ports:
    - protocol: TCP
      port: 80
      targetPort: 9376
  type: LoadBalancer
```

<br>
# Basic Key-Value pair
```
name: John Doe
age: 30
is_employee: true
```
<br>

# Indentation and Nested Structures
```
address:
  street: 123 Main St
  city: Anytown
  country: USA
```
<br>

# List of values
```
skills:
  - Programming
  - Design
  - Management
```
<br>

# Nested Mappings (Map of Maps)


```
contact_info:
  phone_numbers:
    - type: home
      number: "123-456-7890"
    - type: work
      number: "987-654-3210"
  email: johndoe@example.com
```
<br>

# Sequence of Mappings (List of Objects)
```
previous_jobs:
  - title: Developer
    company: TechCorp
    years: 2
  - title: Designer
    company: DesignStudio
    years: 3
```
<br>

# Literal block (|) preserves line breaks
```
description: |
  John Doe is an experienced software developer and designer.
  He has a passion for coding and creative problem solving.
```
<br>

# Folded block (>) folds newlines into spaces
```
bio: >
  John loves working with innovative teams and tackling
  challenging projects to create something truly unique.
```
<br>

# Anchor (&) and Alias (*)
```
default_user: &default_user
  username: johndoe
  password: password123

new_user:
  <<: *default_user  # Merges the default_user values
  role: admin
```
<br>

# Multi-document YAML
---
<br>

# Document 2
```
version: "1.0.0"
features:
  - Easy to read
  - Supports many data types
  - Widely used in Kubernetes and Docker
```
<br>

# Merge Key with << operator
```
base_resources: &base
  cpu: 4
  memory: 16GB

dev_environment:

  <<: *base
  gpu: 1
  additional_storage: 500GB
```
<br>

# Inline Flow Style (JSON-like)
```
person: {name: Jane Doe, age: 28, profession: Designer}
fruits: [apple, banana, cherry]
```
<br>

# Explicit Data Types using Tags
```
int_value: !!int 42       # Explicit integer type
float_value: !!float 3.14 # Explicit float type
string_value: !!str "Hello World" # Explicit string type
```
<br>

# Null values (represented as null, ~, or blank)
```
config: null
timeout: ~
```
<br>

# Boolean values (true/false or yes/no or on/off)
```
is_valid: yes
is_active: true
debug_mode: off
```
<br>

# Date and Time
```
created_at: 2024-10-16
updated_at: 2024-10-16T12:00:00Z
```
<br>
# Complex Structure (Map of Sequences)
```
servers:
  - host: webserver1
    ports: [80, 443]
  - host: webserver2
    ports:
      - http: 8080
      - https: 8443
```

<br>
# Custom Tags for Sequences and Mappings
```
custom_list: !!seq
  - item1
  - item2

custom_map: !!map
  key1: value1
  key2: value2
```