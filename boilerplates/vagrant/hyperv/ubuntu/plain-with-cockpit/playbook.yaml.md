```yaml
---
- hosts: all
  become: yes
  tasks:
  - name: install cockpit
    apt:
      name: cockpit
      update_cache: yes
```
