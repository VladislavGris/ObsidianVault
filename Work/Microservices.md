---
tags:
  - notes
info:
  - passwords
  - services
  - ssh
---
### Test

User: 
```
dockeradm
```
Password:
```
Armadill0!#
```
Test hosts:
10.10.19.5 jiratest.okbtsp.com
10.10.19.8 repotest.okbtsp.com
10.10.19.7 wikitest.okbtsp.com
10.10.19.6 jfrogtest.okbtsp.com
10.10.19.9 bambootest.okbtsp.com
10.10.19.4 chattest.okbtsp.com
### Production

User: 
```
dockeradm
```
Password:
```
Armadill0!#
```
Hosts:
jira.okbtsp.com
repo.okbtsp.com
wiki.okbtsp.com
jfrog.okbtsp.com
bamboo.okbtsp.com
chat.okbtsp.com
10.10.19.30 bamboo.agent.1.okbtsp.com
10.10.19.31 bamboo.agent.2.okbtsp.com
10.10.19.32 bamboo.agent.3.okbtsp.com
10.10.19.33 bamboo.agent.4.okbtsp.com
10.10.19.27 bamboo.agent.5.okbtsp.com
Run bamboo agent: java -Dbamboo.home=/home/bamboo/bamboo-agent-home -jar atlassian-bamboo-agent-installer-10.2.0.jar https://bamboo.okbtsp.com/agentServer/

### Run bamboo-agent after reboot
- Create autostart.sh in bamboo-agent-home directory with code
``` bash
java -Dbamboo.home=/home/bamboo/bamboo-agent-home -jar /home/bamboo/bamboo-agent-home/atlassian-bamboo-agent-installer-10.2.0.jar https://bamboo.okbtsp.com/agentServer/
```
- Run `crontab -e`
- Paste following line:
```
@reboot /home/bamboo/bamboo-agent-home/autostart.sh
```
