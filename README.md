



### **Step 1: Backup the `swarm.pem` File**

The `swarm.pem` file is critical as it contains your Gensyn node's identity. Follow these steps to back it up:

1. **Locate the File**:
   - The `swarm.pem` file is located in the directory where RL-Swarm is installed, typically at `/root/rl-swarm/` or `$HOME/rl-swarm/`.

2. **Copy the File Using Termius SFTP**:
   - Open Termius and connect to your VPS.
   - Navigate to the RL-Swarm folder (`/root/rl-swarm/` or `$HOME/rl-swarm/`) using the Termius SFTP interface.
   - Drag and drop the `swarm.pem` file from the VPS to a secure backup location on your local machine.
  
     

https://github.com/user-attachments/assets/3a8b01b1-f6b2-473a-90f6-e420da6e228e



3. **Verify Backup**:
   - Ensure that the file has been successfully copied and is accessible in its new location.

---

### **Step 2: Delete the Current RL-Swarm Folder**

To start fresh, remove the existing RL-Swarm folder:

1. **Stop the Node**:
   - If your node is running in a screen session, stop it using:
     ```bash
     screen -XS gensyn quit
     ```

2. **Delete the Folder**:
   - Remove the RL-Swarm directory:
     ```bash
     rm -rf $HOME/rl-swarm
     ```

---

### **Step 3: Reinstall RL-Swarm**

Reinstalling ensures a clean setup of your Gensyn Testnet node.

#### **1. Install Dependencies**
Run the following commands to install all necessary dependencies:

```bash
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl screen git yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install -y yarn
```

#### **2. Clone the Repository**
Clone a fresh copy of the RL-Swarm repository:

```bash
git clone https://github.com/zunxbt/gensyn-testnet.git $HOME/rl-swarm
cd $HOME/rl-swarm
```

#### **3. Create a Screen Session**
Start a new screen session to run RL-Swarm in the background:

```bash
screen -S gensyn
```

---

### **Step 4: Restore `swarm.pem` File Using Termius SFTP**

After reinstalling RL-Swarm, restore your `swarm.pem` file:

1. **Open Termius SFTP**:
   - Connect to your VPS using Termius.
   - Navigate to `/root/rl-swarm/` or `$HOME/rl-swarm/`.

2. **Drag and Drop**:
   - Drag and drop your backed-up `swarm.pem` file from your local machine into the RL-Swarm folder on your VPS.

3. **Verify Restoration**:
   - Confirm that `swarm.pem` is now present in the appropriate directory on your VPS.

---

### **Step 5: Start RL-Swarm**

After restoring `swarm.pem`, start RL-Swarm:

1. **Activate Python Virtual Environment**:
   ```bash
   cd $HOME/rl-swarm
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. **Run RL-Swarm Script**:
   ```bash
   ./run_rl_swarm.sh
   ```

- During setup, you may be prompted with:
  ```
  Would you like to push models you train in the RL swarm to Hugging Face Hub? [y/N]
  ```
  Respond with `N`.

---

### Additional Notes

- **Ngrok Integration**:
  The repository already uses Ngrok for remote access, so no need for SSH port forwarding.
- **Detach Screen Session**:
  Let your node run in the background by detaching from the screen session:
  ```bash
  Ctrl + A + D
  ```

This process ensures a clean reinstall while securely restoring your `swarm.pem` file using Termius SFTP.

---
