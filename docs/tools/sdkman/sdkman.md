---
layout: default
title: sdkman
nav_order: 4
has_children: true
permalink: /docs/tools/sdkman
parent: Tools
---
## Sdkman Note

## Installation Java

### 1. List Java

```bash
sdk list java
```

### 2. Install Java

```bash
sdk install java 21.0.2-tem
```

### 3. Show Current 

```bash
sdk current
```

## Env

### 1. Create Environment

    sdk env init

    vi . sdkmanrc

    java=21.0.2-tem   

### 2. Swith Environment

```bash
sdk env
```
### 3. Swith Back to Default

```bash
sdk env clear
```



## References
---
[Install Sdkman](https://sdkman.io/install)