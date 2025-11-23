# Networking (VPC)
## VPC
- We have IGW & Nat Gateway (has elastic IP)
- Public Subnets (VMs with public Ip & private IP)
- Private Subnets (VMs with private IP)

- Connection from VM-public to client
    - IGW used to translate the public accessed ip to the vm private IP
    - No direct connection between the VM and client
    - 2 way communication can be started

- Connection from VM-private to google
    - vm send request to nat gateway 
    - Nat do its magic and  replace source ip
    - nat use IGW to talk to google
    - and the connection goes back
    - Only one way connection, only the private vm can init the connect (security)
    - Nat keep a `mapping entry` to keep track of its connections

- Security Groups:
    - Allow rules only — everything else is implicitly denied.
- NACL:
    - Can explicitly allow or deny traffic


## NATing
- `SNAT` changes the ***source IP*** address of a packet as it leaves your network. (*MASQUERADE*)
- `DNAT` changes the ***destination IP*** address of a packet as it enters your network.

## Firewall stateful VS statless
- `Stateful`: When a connection is allowed through the firewall in either direction, return traffic matching session table is also allowed
    - ex: if allow tcp port 80, the response will be allowed even it not explicitly defined

- `Statless`: Does not track connection state. Each packet is evaluated independently based only on rules.
    - ex: if allow tcp port 80 the response will not be permitted unless an explicit defined incoming rule.

# Security In Cloud
- Secure network(sg, nacl, firewall rules)
- secure access (RBAC, Identity federation)
- Secure app secrets & Config (Secret Manager)
- Encryption in rest & Transient (KMS, AWS Certificate Manager)
- Logs/metircs (cloud Trail)


# Resilience VS Fault tolerance VS High Availability VS Reliability

***`Durability = Data does not get lost.`***

***`Reliability = system  perform its intended function correctly over time.`*** 

***`Resilience = system  recover quickly from failures and return to normal operation.`***

***`Scalability = System can grow when demand increases.`***

***`High availability = system recovers quickly from failures, but might have a brief disruption(Downtime).`***

***`Fault tolerance = Continuous operation under failure & Zero DownTime`***

--- 

| Concept               | Meaning (Simple)                 | AWS Example                |
| --------------------- | -------------------------------- | ---------------------------|
| **Durability**        | Data never gets lost             | S3                         |
| **Reliability**       | Works correctly over time        | Lambda                     |
| **Resilience**        | Recovers from failures           | Auto Scaling Group         |
| **Scalability**       | Grows with traffic               | DynamoDB                   |
| **High Availability** | Minimal downtime during failover | RDS Multi-AZ               |
| **Fault Tolerance**   | Zero downtime under failure      | S3, DynamoDB Global Tables |


# Observability
<div style="text-align: center;"><img src="./observability.png" alt="three-tier design" width="1000 " height="450" style="border-radius: 15px;"></div>  

# CloudWatch
- Collection of monitoring tools 
<div style="text-align: center;"><img src="./CloudWatch.png" alt="three-tier design" width="900 " height="350" style="border-radius: 15px;"></div>

- Logs, Metrics, Events, Alarms, Dashboards
- **Logs**
    - We can have Logs, Logs Groups, Log Streams
- **Metrics**
    - Create Custom metrics and define resolution (intervale to connect data)
    - not all ec2 metrics are tracked without an agent (need to install cloudwatch agent on Ec2)
- **EventsBridge**:
    - Event
    - Producer
    - Event Bus (Place that contain events)
    - Rules (determine what events to deliver)
    - Targets (the target consume events)
    - common use case: (Trigger DB Backup everyday)
<div style="text-align: center;"><img src="./eventbridge.png" alt="three-tier design" width="800" height="400" style="border-radius: 15px;"></div>

- **Alarm**:
    - state (OK, ALARM, INSUFFICIENT)
    - Condition (define threshold -> `Static & Anomaly`)
    - Action (Notifications, ASG, EC2 Actions)

# CLoudTrail
- Monitor API calls and Actions
- we use it to identify:
    - who User, UserAgent
    - Where Source IP Address
    - When EventTime
    - What Region, resource

- It tracks Management Events (Default) , Data Events


# Linux

## Network
- IP commands (link, route, address) -> Temp Change
- netplan -> Permanent network change 
- Net Troubleshooting -> `ss`, `netstate`, `tcpdump`

- DNS -> `resolved.conf`, `resolvectl`, `/etc/hosts`
- DNS Troubleshooting -> `nslookup`, `dig`

- Firewall `ufw`, `PortForward Iptables`


# Git
- VCS Version Control System
- We start with `git init`
- We have current working dir, Staging Area, Local Repo
- Use  `git add` : working dir -> staging Area
- Use `git commit` : staging Area -> Local Repo
- We use commit to create a version of our Code
- Version = Commit, has history that tell who did this version 
- We set username/email to `git config --global`, this will appear in commits
- Modify our last commit, We use `--amend` 
- We use `git reset` & based on mode **soft**, **mixed** & **hard**:  
    - When `passing HEAD` undo last commit, with/without staging, with/without working dir
    - No `HEAD` passing undo with/without staging, with/without working dir
- To move between commit and version use use `git commit <commit-it>`
- ***git pull is git fetch + git merge***
    - git fetch -> only bring commit history & branches
    - git pull -> also merge this changes to working dir

- Merge & Branch
    - We create a branch to make a changes not in the main code/branch
    - Merge is combining the changes of both branches into the current working branch
    - Confect is merging two changes of same line 

- merge, git use three way merge
    - BASE       (common ancestor)
    - MAIN       (current branch)
    - BRANCH B   (other branch)

- Feature Branch Workflow:
1. create feature branch
2. push it to remote
3. Create PR Pull Request
4. Merge Feature branch to master after review

- Our main to concerns is:
    - How to keep the feature branch up to date with Main
    - How to Move changes from feature branch -> Main branch
- We use `fetch` as safe way to get only commit history changed on remote
- Clean history we use rebase to make our history liner 
- When we want to merge we merge into feature first then we do whatever in feature branch and  when we merge back to main, we already resolved  the conflict at the branch side and it created a commit for it 

## Reset
- ***Reset*** operation rewrites commit history by moving the HEAD pointer.
- it undo commits without create a new ones.
    - `soft`: undo last commit, keep staged changes and changes in working dir
    - `mixed`: undo last commit & unstage changes, keep changes in working dir
    - `hard`: undo last commit & unstage changes & undo changes in working dir 
- When no head passed, we can so the same but on the current staged changes and changes in working dir

```bash
git reset --soft HEAD~1                     # Undo Last Commit (keep changes staged)
git reset --mixed HEAD~1                    # Undo Last Commit (unstage changes)
git reset --hard HEAD~1                     # Undo Last Commit Completely (removes the last commit, its staged and working directory changes.)
```

### Revert
- undo changes by creating a new commit that reverses the effect of a previous commit
- Create a new commit that undo the changes of another commit
```bash
git revert HEAD                             # Revert the last commit
git revert <commit-hash>                    # Revert specific command
git revert --no-edit <commit-hash>          # Skips the commit message editor
git revert --no-commit <commit-hash>        # Applies changes to your working directory without committing them.
git revert <old-commit>^..<new-commit>      # Reverts a range of commits (from old to new)
```
