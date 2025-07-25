# gensyn
Gensyn Testnet Node Guide
💻 System Requirements
Requirement	Details
CPU Architecture	arm64 or amd64
Recommended RAM	24 GB
CUDA Devices (Recommended)	RTX 3090, RTX 4070, RTX 4090, A100, H100
Python Version	Python >= 3.10 (For Mac, you may need to upgrade)
🌐 Rent GPU
Note

Renting GPU is not necessarily needed, you can still run this node on VPS or on WSL, but you may face OOM error plus you may have less winning rate, that is why my recommendation is renting a GPU if you can, otherwise you can proceed with VPS or WSL.

Visit : Quick Pod Website
Sign Up using email address
Go to your email and verify your Quick Pod account
Click on Add button in the corner to deposit fund
You can deposit using crypto currency (from metamask) or using Credit card
Now go to template section and then select Ubuntu 22.04 jammy in the below
Now click on Select GPU and search RTX 4090 and choose it
Now choose a GPU and click on Create POD button
Your GPU server will be deployed soon
You can simply click on Connect button and then choose Connect to Web Terminal
But if you are using different gpu provider then you should use Connect via SSH method mentioned below
🛜 Connect via SSH (Only for GPU)
Note

This step is only required if you running this node on GPU, if you want to use VPS or WSL, then skip this step and login to your VPS server using username and password which u received from the VPS provider and then move to installation section

First open a terminal (this could be either WSL / Codespace / Command Prompt)
Use this below command to generate SSH-Key
ssh-keygen
It will ask 3 questions like this :
Enter file in which to save the key (/home/codespace/.ssh/id_rsa):
Enter passphrase (empty for no passphrase):
Enter same passphrase again: 
You need to press Enter 3 times
After that you will get a message like this on your terminal
Your public key has been saved in /home/codespace/.ssh/id_rsa.pub
/home/codespace/.ssh/id_rsa.pub is the path of this public key in my case, in your case it might be different
Screenshot 2025-04-08 081948

You should use this command to see those ssh key :
If you are using Linux/macOS (WSL) : cat path/of/that/publickey , in my case, it would be : cat /home/codespace/.ssh/id_rsa.pub
If you are using Command Prompt : type path\of\that\publickey, in my case, it would be : type \home\codespace\.ssh\id_rsa.pub
If you are using PowerShell : Get-Content path\of\that\publickey, in my case, it would be : Get-Content \home\codespace\.ssh\id_rsa.pub
Now copy this public key and go to hosting provider from where you bought GPU
After visiting the web hosting provider website, navigate to settings and there paste and save your ssh key
Now, copy the command you received after renting the GPU instance and paste it into the terminal where you generated the public key.
In my case, the command looks like this:
ssh -p 69 root@69.69.69.69
Now paste this command on this terminal to access your GPU server
📥 Installation
Install sudo
apt update && apt install -y sudo
Install other dependencies
sudo apt update && sudo apt install -y python3 python3-venv python3-pip curl wget screen git lsof nano unzip
Install Node.js and npm
curl -sSL https://raw.githubusercontent.com/zunxbt/installation/main/node.sh | bash
Create a screen session
screen -S gensyn
Run the swarm
cd $HOME && rm -rf gensyn-testnet && git clone https://github.com/zunxbt/gensyn-testnet.git && chmod +x gensyn-testnet/gensyn.sh && ./gensyn-testnet/gensyn.sh
It will ask some questions, you should send response properly
Would you like to push models you train in the RL swarm to the Hugging Face Hub? [y/N] : Write N
When you will see interface like this, you can detach from this screen session
Screenshot 2025-04-01 061641

Detach from screen session
Use Ctrl + A and then press D to detach from this screen session.
🔄️ Back up swarm.pem
After running the Gensyn node, it is essential to back up the swarm.pem file from your remote server (GPU or VPS) to your local PC. If you lose this file, your contribution will also be lost. I will mention 2 method , 1 is simpler but not that much secure and another one is secure but a lil bit complex for the beginners

Method 1 (Very Simple)
First make sure that you are in rl-swarm folder and then run this command
[ -f backup.sh ] && rm backup.sh; curl -sSL -O https://raw.githubusercontent.com/zunxbt/gensyn-testnet/main/backup.sh && chmod +x backup.sh && ./backup.sh
It will show something like this in your terminal
image

1️⃣ VPS/GPU/WSL to PC

If you want to backup swarm.pem(Must), userData.json (Optional), userApiKey.json (Optional) from VPS/GPU/WSL to your PC then simply visit the URL (don't use the commands mentioned below) and press Ctrl + S to save these files.
2️⃣ One VPS/GPU/WSL to another VPS/GPU/WSL

If you want to backup swarm.pem(Must), userData.json (Optional), userApiKey.json (Optional) from One VPS/GPU/WSL to another VPS/GPU/WSL then simply use the commands on another VPS/GPU/WSL where you want to use these files.
Method 2 (Manual)
If you face any issue with this automated back up process then it is recommended to use manual guide : Click Here

🟢 Node Status
1. Check Logs
To check whether your node is running or not, you can check logs
To check logs you need to re-attach with screen session, so use the below command
screen -r gensyn
If you see everything running then it's fine
Now detach from this screen session, Use Ctrl + A and then press D to detach from this screen session.
Everytime you reattach, every time you should detach
2. Check Wins
Visit : https://gensyn-node.vercel.app/
Enter Peer-ID that you often see this in your logs
The more win, the better
Note



