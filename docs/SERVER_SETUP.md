# Server Setup

Tracks the steps taken to provision and harden the Lightsail server. Update the checkboxes as each step is completed so this file always reflects the real state of the server.

## 1. Lightsail Instance

- [x] Instance created: `bayone-answer-engine`
- [x] Region: Asia Pacific (Mumbai), ap-south-1
- [x] Blueprint: Linux operating system → Ubuntu 24.04 LTS
- [x] Plan: $12/month (2 GB RAM, 2 vCPUs, 60 GB SSD)
- [ ] Static IP created and attached
- [ ] Firewall restricted to SSH only (port 22), all other rules removed

## 2. OS Hardening

Run over SSH (Lightsail console → instance → Connect using SSH):

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install unattended-upgrades -y
sudo dpkg-reconfigure --priority=low unattended-upgrades
```

- [ ] System packages updated
- [ ] Automatic security updates enabled
- [ ] Lightsail snapshot #1 taken (post-hardening, pre-Hermes baseline)

## 3. Hermes Install

- [ ] Hermes installed via official installer
- [ ] OpenRouter API key configured in Hermes config
- [ ] Smoke test passed: agent responds to a manual prompt via OpenRouter

## 4. GitHub Connection (Server Side)

- [ ] Deploy key generated on the server (`ssh-keygen`, no passphrase, dedicated key — do not reuse your laptop's key)
- [ ] Public key added to the GitHub repo under Settings → Deploy keys, **read-only access only**
- [ ] `git clone` (first time) / `git pull` (subsequent) tested successfully on the server

## 5. Google Sheets Connection

- [ ] Service-account JSON uploaded to the server (via `scp` or pasted directly in an SSH session — never via a committed file)
- [ ] JSON stored outside the git-tracked folder, permissions locked to owner-read-only (`chmod 600`)
- [ ] Test write to the Google Sheet succeeds from the server

## 6. Apify Connection

- [ ] Apify API token configured in Hermes config
- [ ] Test call to `trudax/reddit-scraper-lite` succeeds from the server
- [ ] Test call to `harshmaur/reddit-scraper` succeeds from the server

## 7. Snapshots & Ongoing Hygiene

- [ ] Snapshot taken after Sprint 1 complete (monitoring skeleton working end to end)
- [ ] Snapshot taken after Sprint 2 complete (scoring + drafting working)
- [ ] Monthly billing review against the $20 AWS budget alert
- [ ] Monthly key rotation review

---

**Reminder:** this server should never expose a web-facing port, should never run any third-party skill packs, and should hold secrets only in local server config — never in this repository.
