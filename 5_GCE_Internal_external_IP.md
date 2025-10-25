# Internal and External IP Addresses in Google Cloud Compute Engine

When you create a Virtual Machine (VM) instance in **Google Cloud Compute Engine (GCE)**, it is assigned **IP addresses** that allow it to communicate with other resources. There are two types of IP addresses associated with a VM:

1. **Internal IP Address**
2. **External IP Address**

Let's dive into each of them in detail.

---

## 1. Internal IP Address

- **Definition:**  
  An internal IP address is used **inside the Google Cloud network** (or any corporate/private network). It allows VMs to communicate with each other within the same network.

- **Key Characteristics:**
  - Assigned by default to every VM instance.
  - Not accessible from the internet.
  - Can be the same across different networks, as they are private.
  - Remains **static** for the VM even if the VM is stopped and restarted.

- **Example:**  
Internal IP: 10.128.0.2

You can only use this IP inside the Google Cloud network. You cannot send requests to it from the internet.

---

## 2. External IP Address

- **Definition:**  
An external IP address is **internet addressable**. This allows you to access your VM from anywhere on the internet.

- **Key Characteristics:**
- Optional: you can choose whether a VM should have an external IP.
- Must be unique across the internet.
- Changes when the VM is stopped and restarted **unless you reserve a static external IP**.
- Used for SSH, HTTP, or any service that needs to be accessible from the internet.

- **Example:**  
External IP: 34.123.6.112

You can reach your VM using this IP from your browser or other internet-connected devices.

---

## 3. Behavior When Stopping and Starting a VM

1. **Internal IP:**  
 - Remains the same even if the VM is stopped and restarted.
 - Ensures internal communications are uninterrupted.

2. **External IP:**  
 - Changes when the VM is stopped and restarted.
 - Any previous external connections (like SSH or HTTP requests) using the old IP will fail.
 - You will need the new external IP to access the VM again.

**Example Flow:**

1. VM running:
 - Internal IP: 10.128.0.2
 - External IP: 34.123.6.112
2. Stop VM:
 - Internal IP: 10.128.0.2 (unchanged)
 - External IP: None
3. Start VM again:
 - Internal IP: 10.128.0.2
 - External IP: 34.124.7.113 (new external IP)

> ⚠️ Note: The changing external IP can break connections like SSH or web services. To prevent this, you can **reserve a static external IP**.

---

## 4. Practical Demonstration

1. **Stop and Start VM:**  
 - Internal IP remains the same.
 - External IP changes.
 - SSH connections using the old external IP will fail.

2. **Restart Services:**  
 - After a restart, you may need to restart services (e.g., Apache server) on the VM.
 ```bash
 sudo su
 service apache2 start
