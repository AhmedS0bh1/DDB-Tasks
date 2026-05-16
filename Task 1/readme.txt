# 🚀 Distributed Database Tasks - Golang

This project is a Distributed Systems application built using **Go (Golang)**. It focuses on creating a centralized control system (Master/Controller) to manage multiple machines (Workers/Agents) and execute remote tasks over a network using the TCP protocol and JSON for data exchange.

---

## ✨ Features

**Task 1** is fully implemented using a Controller-Agent architecture and includes the following operations:
* 🔒 **Lock Workstation:** Simultaneously lock the screens of all connected devices.
* 🛑 **Remote Shutdown:** Turn off all connected devices remotely.
* 🖼️ **Change Wallpaper:** Change the desktop background of all connected devices by selecting an image on the Controller and broadcasting it.
* 📁 **File Distribution:** Send any file from the Controller to be automatically received and saved on all connected Agent machines.

---

## 🛠️ Prerequisites

* [Go (Golang)](https://golang.org/dl/) version 1.18 or higher installed.
* Windows operating system for the target machines (Agents) to ensure the `shutdown` and Registry (`reg`) commands for wallpaper changes work correctly. *(Note: The code can be easily modified to support Linux commands).*

---

## 📂 Project Structure

The project consists of two main files:
1. `controller.go`: Acts as the Server (Master Node) that accepts incoming connections and broadcasts commands.
2. `agent.go`: Acts as the Client (Worker Node) that runs in the background on the target machines to receive and execute commands.

---

## 🚀 How to Run

### 1. Run the Controller (Master Node)
Open your terminal in the project directory and run the following command:
```bash
go run controller.go -port 9000

Note: By default, the server listens on port 9000 and waits for agent connections.

2. Run the Agent (Target Machines)
If you are testing the Agent on the same machine:

go run agent.go

If you are running the Agent on a different machine within the same network, open the agent.go file and update this line with the IP address of the Controller machine:
conn, err := net.Dial("tcp", "192.168.1.x:9000") // Replace with the Controller's IP
🎮 Usage
Once the Controller is running and at least one Agent is connected, an interactive menu will appear in the Controller's terminal:

--- Controller Menu ---
1. Lock all connected devices
2. Shutdown all connected devices
3. Change wallpaper on all connected devices
4. Show connected devices
5. Exit
6. Send a file to all connected devices

Choose a number:
For Changing Wallpaper (Option 3): A file picker dialog will open on your machine. Select an image, and it will be automatically encoded and distributed.

For Sending a File (Option 6): You will be prompted to enter the full absolute path of the file (e.g., C:\Users\Public\document.pdf). The file will be saved on the Agents' machines prefixed with received_ (e.g., received_document.pdf).

⚙️ Future Enhancements
Task 2 Implementation: Add MapReduce capabilities for distributed data querying or build a simplified Google File System (GFS).

Task 3 Implementation: Introduce Consistent Hashing to effectively distribute and balance data across multiple nodes.

Security: Add TLS/SSL encryption to secure the network traffic and file transfers between the Controller and the Agents.
