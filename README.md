# airchains-node

### **Step 1: Install Prerequisites**

Before you can set up a full node, you need to ensure your environment is set up correctly. You will need:

- A Linux-based server (Ubuntu is recommended)
- `git`, `curl`, and `jq` installed
- **Docker** and **Docker Compose** to manage containers

Run the following commands to install the required tools:

```bash
# Update the package list
sudo apt update

# Install required tools
sudo apt install -y git curl jq

# Install Docker
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# Install Docker Compose
sudo curl -L "https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# Verify Docker installation
docker --version
docker-compose --version
```

---

### **Step 2: Clone the Airchains Repository**

Next, you need to clone the Airchains Junction repository, which contains everything needed to run the node.

```bash
# Clone the Airchains Junction repository
git clone https://github.com/airchains/airchains-junction.git

# Change directory to the cloned repository
cd airchains-junction
```

---

### **Step 3: Configure Environment Variables**

The configuration file `env` must be set up correctly to run your full node. Here is an example of what the environment variables might look like (you can modify this based on your specific requirements):

```bash
# Create an environment file from the template
cp .env.example .env

# Open and edit the file with your text editor (e.g., nano or vim)
nano .env
```

Edit the `.env` file to match your node settings, such as the **network**, **chain ID**, and any other specific configurations required by Airchains.

Example variables might include:

```bash
NODE_NAME="MyNode"
CHAIN_ID="airchains-1"
RPC_PORT=26657
P2P_PORT=26656
GRPC_PORT=9090
```

After editing, save and close the file.

---

### **Step 4: Run the Docker Setup**

With the repository cloned and environment variables configured, you can now run the full node using Docker.

```bash
# Start the full node
docker-compose up -d
```

This will pull the necessary Docker images, set up the blockchain node, and run it in the background.

---

### **Step 5: Check Node Logs**

To ensure that the node is running correctly, you should check the logs of your node. Use the following command:

```bash
# Check logs for the full node
docker-compose logs -f
```

Look for logs indicating that your node is successfully syncing blocks and connected to peers.

---

### **Step 6: Verify the Node is Running**

You can check if your node is running and synchronized by querying its RPC endpoint. You can use `curl` to make an RPC request to your node:

```bash
# Query the node's status via RPC
curl http://localhost:26657/status
```

The output will give you details about the node’s syncing status, block height, and other key information. Make sure your node is connected to peers and is processing blocks.

---

### **Step 7: Set Up Monitoring (Optional)**

For long-term node operation, it’s useful to set up monitoring tools like **Prometheus** or **Grafana** to visualize the performance of your node and track metrics such as CPU usage, memory usage, block height, and peer connectivity.

---

### **Step 8: Troubleshooting**

If you encounter issues while running your full node, try the following steps:

- Check the Docker logs (`docker-compose logs -f`) to identify any errors.
- Ensure that all ports specified in the `.env` file are open and not blocked by firewalls.
- If synchronization issues arise, ensure your server has sufficient disk space and network bandwidth.

---

### **Step 9: Stopping the Node**

If you need to stop the node for maintenance or updates, you can do so by running the following command:

```bash
# Stop the full node
docker-compose down
```

This will stop and remove the running containers, but it will not delete the blockchain data unless you explicitly remove the volumes.
