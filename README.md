# advanced-network-automation-workshop

This immersive, hands-on workshop highlights the power and capabilities of AAP in automating real-world network scenarios. As a continuation of the Introduction to Ansible Network workshop, this session introduces advanced concepts, including Source of Truth (SoT), dynamic inventories, compliance, configuration drift, and state validation. Rather than focusing on extensive playbook development from scratch, participants will explore the "art of the possible" by building workflows to deploy and validate a multi-vendor EVPN VXLAN switching fabric.

**Owner:** andubiel
**Migrated from:** https://github.com/rhpds/advanced-network-automation-workshop/

---

## What was set up

1. Repository created (migrated from existing Showroom repo)
2. `catalog-info.yaml` added to repository
3. Registered in Developer Hub catalog
4. Orchestrator workflow started — your AI-guided content pipeline is running!

## What happens next

Claude will walk you through the entire content lifecycle — from intake and spec creation, through Jira tracking and reviews, all the way to a published lab on RHDP. Just follow the prompts!

## Getting started

### DevSpaces (recommended)

1. Open in DevSpaces: `https://devspaces.apps.ocpv-infra02.wdc07.infra.demo.redhat.com#https://github.com/rhpds/advanced-network-automation-workshop`
2. Use Claude via the **extension** or the **CLI**:
   - **Extension:** Click the **Claude** icon in the sidebar, click **New Session**. If the Claude icon is not visible, open **Extensions** (`Ctrl/Cmd+Shift+X`), find **Claude Code for VS Code** under the DevSpaces section, click it, then click **Enable (Workspace)**.
   - **CLI:** Open a terminal and run `claude`
3. Run `/rhdp-publishing-house` — and you're off!

### Local machine

1. Install the skills:
   ```
   git clone -b prod https://github.com/rhpds/rhdp-publishing-house-skills.git ~/.claude/skills/publishing-house
   ```
2. Clone the repo:
   ```
   git clone https://github.com/rhpds/advanced-network-automation-workshop
   ```
3. `cd advanced-network-automation-workshop`
4. Start Claude CLI: `claude`
5. Run `/rhdp-publishing-house` — and you're off!

## Useful commands

### Check memory pressure on the containerlab VM

Run on the containerlab VM to see whether the topology and Netbox are competing for memory:

```
free -h                                            # overall memory and swap use
docker stats --no-stream                           # per-container memory use
sudo dmesg -T | grep -i -E 'oom|killed process'    # processes killed by the OOM killer
```

If `dmesg` shows OOM kills, cap the Netbox stack with `mem_limit` and `oom_score_adj` in `netbox-docker/docker-compose.override.yml` so the kernel reclaims memory from Netbox before the network nodes.

### Inspect or redeploy the containerlab topology

Run on the containerlab VM:

```
sudo clab inspect /home/lab-user/2_multi_vendor_vxlan     # show node names, state, and management IPs
sudo clab redeploy /home/lab-user/2_multi_vendor_vxlan    # destroy and recreate all nodes
```

`redeploy` recreates every node from its startup config, so it wipes any configuration pushed during the lab. Don't run it while a student is mid-lab.
