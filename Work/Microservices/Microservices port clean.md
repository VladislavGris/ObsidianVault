---
tags:
  - work
  - tasknote
info:
  - services
---
## Related notes:
- [[Microservices]]

## Ports removed
### Jira

List of ports, used in jira traefik container:
```yml
    ports:
      - "80:80"
      - "8080:8080"
      - "443:443"
      - "465:465"
      - "587:587"
      - "993:993"
      - "25:25"
      - "143:143"
      - "9090:9090"
      - "9001:9001"
```
Now:
```yml
    ports:
      - "80:80"
      - "443:443"
```

### Confluence

Original:
```yml
	ports:
      - "80:80"
      - "8080:8080"
      - "443:443"
      - "465:465"
      - "587:587"
      - "993:993"
      - "25:25"
      - "143:143"
      - "9090:9090"
      - "9001:9001"
```
New:
```yml
	ports:
      - "80:80"
      - "443:443"
```

### Bitbucket

Original:
```yml
    ports:
      - "80:80"
      - "8080:8080"
      - "443:443"
      - "465:465"
      - "587:587"
      - "993:993"
      - "25:25"
      - "143:143"
      - "9090:9090"
      - "9001:9001"
```
New:
```yml
	ports:
      - "80:80"
      - "443:443"
```
- Removed **elasticsearch** container *(removed support in bitbucket 9)*

### Bamboo

Original:
```yml
	ports:
      - "80:80"
      - "8080:8080"
      - "443:443"
      - "465:465"
      - "587:587"
      - "993:993"
      - "25:25"
      - "143:143"
      - "9090:9090"
      - "9001:9001"
```
New:
```yml
	ports:
      - "80:80"
      - "443:443"
```

### JFrog

Original:
```yml
	ports:
      - "80:80"
      - "8080:8080"
      - "443:443"
      - "465:465"
      - "587:587"
      - "993:993"
      - "25:25"
      - "143:143"
      - "9090:9090" 
      - "9001:9001"
```
New:
```yml
	ports:
      - "80:80"
      - "443:443"
```