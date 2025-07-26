# -OG--Node-Auto-RPC-Script

# ðŸš€ OG LABS Node Auto RPC Setup
**By Thakur Saab ðŸ† â€“ Gujarat, India**

A full setup guide to install, sync, and monitor your 0G Storage Node in minutes. Includes auto RPC setup and Flow DB snapshot sync.

---

## ðŸ“‹ System Requirements

- **Ubuntu 20.04 or 22.04**
- **4+ Cores CPU**
- **16 GB+ RAM**
- **500GB â€“ 1TB SSD or NVMe**
- **Public IPv4**

---

## ðŸ”§ Step 1 â€“ Start a Screen Session

```bash
screen -S og
```

---

## ðŸ“¦ Step 2 â€“ Update System & Install Git

```bash
sudo apt update && sudo apt install git -y
```

---

## âš™ï¸ Step 3 â€“ Install 0G Storage Node

```bash
bash <( curl -sL https://raw.githubusercontent.com/CodeDialect/0g-Storage-Node/main/0g_node_setup.sh          | sed '/^[ _|\/()]+$/d;/figlet/d;/toilet/d' )      && echo && echo "============================================"      && echo "       Made by Thakur Saab, Gujarat "      && echo "============================================"
```

---

## ðŸŒ Step 4 â€“ Apply Custom RPC

```bash
bash <(curl -sL https://raw.githubusercontent.com/CodeDialect/0g-Storage-Node/main/change_rpc.sh)
```

**ðŸ”— Recommended RPC:**  
```
https://0g-evmrpc.sr20de.xyz/
```

---

## âš¡ Step 5 â€“ Fast Sync with Flow DB Snapshot

### ðŸ›‘ Stop Node

```bash
sudo systemctl stop zgs
```

### ðŸ§¹ Remove Old Flow DB

```bash
rm -rf $HOME/0g-storage-node/run/db/flow_db
```

### ðŸ“¥ Download & Extract Snapshot

```bash
wget https://github.com/Naveenrawde3/0G-LABS-STORAGE-NODE-RUN-GUIDE-BY-NTEK/releases/download/v1.0/flow_db.tar.gz   -O $HOME/0g-storage-node/run/db/flow_db.tar.gz &&   tar -xzvf $HOME/0g-storage-node/run/db/flow_db.tar.gz -C $HOME/0g-storage-node/run/db/
```

---

## ðŸ” Step 6 â€“ Restart Node

```bash
sudo systemctl restart zgs
```

---

## ðŸ’¡ Step 7 â€“ Live Sync Status Checker

```bash
while true; do   response=$(curl -s -X POST http://localhost:5678 -H "Content-Type: application/json"   -d '{"jsonrpc":"2.0","method":"zgs_getStatus","params":[],"id":1}');   logSyncHeight=$(echo $response | jq '.result.logSyncHeight');   connectedPeers=$(echo $response | jq '.result.connectedPeers');   echo -e "logSyncHeight: [32m$logSyncHeight[0m, connectedPeers: [34m$connectedPeers[0m";   sleep 5; done
```

ðŸ” This will keep printing `logSyncHeight` & `connectedPeers` every 5 seconds.  
âŒ Press `Ctrl + C` to stop.

---

## ðŸ§° Node Management Commands

| ðŸ”§ Action                | ðŸ§ª Command                                                              |
|-------------------------|-------------------------------------------------------------------------|
| âœ… Check Node Status     | `sudo systemctl status zgs`                                             |
| ðŸ“œ View Logs            | `tail -f ~/0g-storage-node/run/log/zgs.log.$(date +%F)`                 |
| ðŸ›‘ Stop Node            | `sudo systemctl stop zgs`                                               |
| âŒ Remove Node Service   | `sudo systemctl disable zgs && sudo rm /etc/systemd/system/zgs.service` |
| ðŸ§¼ Delete All Node Files | `rm -rf $HOME/0g-storage-node`                                          |
| ðŸ” Reattach to Screen    | `screen -r og`                                                          |

---

## ðŸ¤– Telegram Bot

Check your node status from Telegram:  
ðŸ‘‰ [@OgLab_Checker_bot](https://t.me/OgLab_Checker_bot)

---

## ðŸ«¡ Credits

Made with â¤ï¸ by **Thakur Saab â€“ Gujarat**  
Helping the community automate OG Node deployments âœ¨
