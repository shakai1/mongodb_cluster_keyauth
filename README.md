MongoDB Cluster Setup Playbook

This Ansible playbook automates the installation, configuration, and setup of a MongoDB replica set cluster. It includes tasks for installing MongoDB, configuring a secure replica set, and verifying the cluster's status.

Features
- Installs MongoDB from the official MongoDB repository.
- Configures a secure replica set with a keyfile for authentication.
- Sets up a dedicated data directory with proper permissions and mount options.
- Applies custom MongoDB configurations for optimized performance.
- Initializes the replica set and adds secondary nodes to the cluster.
- Retrieves and displays the replica set status.

Prerequisites
1. Environment:
   - Target nodes should run a Debian-based OS (e.g., Debian Bookworm).
   - Ansible must be installed on the control node.
2. Ansible Configuration:
   - Define the mongodb_nodes group in your Ansible inventory with the IP addresses or hostnames of the MongoDB nodes.
3. Networking:
   - Ensure all nodes can communicate on port 27017.
   - Configure firewall rules to restrict access to trusted hosts only.

Playbook Structure
The playbook is divided into several roles:
1. MongoDB Installation:
   - Adds the official MongoDB repository and installs the required packages.
2. Keyfile Management:
   - Generates a secure keyfile for authentication and distributes it to all nodes.
3. Directory Configuration:
   - Creates and mounts a dedicated data directory for MongoDB.
4. Replica Set Configuration:
   - Applies a custom MongoDB configuration file and initializes the replica set.
5. Validation:
   - Retrieves the replica set status and displays essential information.

Inventory Example
[mongodb_nodes]
mongodb1.example.com
mongodb2.example.com
mongodb3.example.com

Variables
You can customize the following variables in your playbook or inventory:
- replSetName: Name of the MongoDB replica set (default: myReplicaSet).
- dbPath: Path to the MongoDB data directory (default: /mnt/mongodb_data).
- bindIp: IP addresses to bind MongoDB to (default: 0.0.0.0).

Usage
1. Clone this repository or copy the playbook files to your Ansible control node.
2. Update the inventory file with your MongoDB nodes.
3. Run the playbook:
   ansible-playbook -i inventory mongodb_cluster.yml
4. Verify the setup:
   - Use the debug output or manually connect to a MongoDB node to check the replica set status.

Security Notes
- The keyfile used for replica set authentication is generated dynamically and stored securely with appropriate permissions (0400).
- The playbook binds MongoDB to all network interfaces by default. For production environments, restrict access using bindIp and firewalls.
- Ensure no sensitive information (e.g., IP addresses, credentials) is hardcoded or exposed in logs.
