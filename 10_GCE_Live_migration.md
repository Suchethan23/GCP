# 🔄 Live Migration in Compute Engine

## 🔍 What Is Live Migration?
Live Migration is a Compute Engine feature that keeps your VM **running even when Google Cloud performs hardware or software maintenance** on the underlying host machine.

Instead of stopping your VM during maintenance:
- GCP **moves the running VM to a new host**
- The migration happens **within the same zone**
- There is **no downtime** and **no change** to the VM's configuration (IP, disks, metadata, etc.)

This ensures **high availability** for your workload.

---

## ✔️ How Live Migration Works
1. GCP schedules a maintenance event on the host where your VM is running.
2. Your VM is **automatically moved** to another host with available capacity.
3. The move happens seamlessly; your application continues to run without interruption.

Live Migration supports:
- VMs with **local SSDs**
- Most standard machine types

---

## ❌ Live Migration Limitations
Live Migration **is not available** for:
- **Preemptible VMs**  
- **Spot VMs**  
- VMs with **GPUs attached** (GPU workloads require host stability)

---

## 🛠️ Configuring Live Migration

Live Migration settings are configured under **Availability Policy** when creating or editing a VM.

### Availability Policy Settings

#### **1. On-host maintenance**
Determines what happens when GCP performs maintenance.

Options:
- **Migrate (recommended & default)**  
  - VM is moved to another host with no downtime  
- **Terminate**  
  - VM is stopped during maintenance  
  - Useful only for specific workloads that cannot be migrated

#### **2. Automatic restart**
Controls whether the VM should automatically restart if Google Cloud stops it for non-user reasons.

- **On (recommended)**  
  - VM restarts automatically after hardware failure or system maintenance
- **Off**  
  - VM stays stopped until manually restarted

These settings help maintain VM uptime during failures or maintenance events.

---

## 📝 Summary
- Live Migration keeps VMs running during host updates by **moving them to another host**.
- Works seamlessly without changing VM properties.
- Configure under **Availability Policy**:
  - **On-host maintenance: Migrate**
  - **Automatic restart: On**
- Not supported for **Preemptible**, **Spot**, or **GPU-attached** instances.

