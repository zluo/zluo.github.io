---
layout: default
title: python code base
nav_order: 1 
parent: python
grand_parent: Computer Language
---

# Python Code base
---

# File IO

### Read command line arguments

```python
import sys
sys.argv[1]
```

### Get Current Directory

```python
import os
os.getcwd()
```

### Get Absolute Directory

```python
os.path.abspath('/var/lib/python/.././path)
```

### Join Directory

```python
os.path.join(os.getcwd(), sys.argv[1])
```

### Split Directory And File Name

```python
baseDir, fileName  = os.path.split(self.videoFile)
```


### Make Directory

```python
from pathlib import Path
Path(clipsDir).mkdir(parents=True, exist_ok=True)
```

### Check file exists

```python
   if os.path.exists(fileName):
```

### Write file 

```python
with open(self.jsonFile, "w", encoding="utf-8") as writer:
    writer.write(json.dumps(result["segments"]))
```

### Json load and dump

```python
import json 
f = open(self.jsonFile)
data = json.load(f)
```

### Read file line by line

```python
f = open(self.jsonFile, 'r')
for line in f:    
```

```python
f = open(self.jsonFile, 'r')
lines =  f.readlines()
```

