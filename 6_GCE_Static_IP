# Static IP Addresses in Google Cloud Compute Engine

## Overview

A **static IP address** in Google Cloud Compute Engine (GCE) provides a fixed, unchanging external IP for resources such as virtual machine (VM) instances.  
By default, Compute Engine assigns an **ephemeral** (temporary) external IP to instances, which changes when the VM is stopped and restarted.  
Static IPs ensure consistent connectivity and are recommended for production workloads that require stable endpoints.

---

## Types of External IP Addresses

| Type | Description | Behavior on VM Restart |
|------|--------------|------------------------|
| **Ephemeral** | Temporary IP address automatically assigned when a VM instance is created. | Released and reassigned after VM stop/start. |
| **Static** | Reserved IP address that remains fixed until explicitly released. | Remains unchanged across VM restarts. |

---

## Use Cases

- Hosting web applications or APIs that require a persistent public endpoint.  
- Setting up DNS records that point to a consistent IP address.  
- Maintaining stable connectivity between external services and VM instances.  
- Avoiding downtime caused by dynamic IP reassignment.

---

## Reserving a Static IP Address

### Prerequisites

- A Google Cloud project with **Compute Engine** and **VPC Network** APIs enabled.  
- Appropriate IAM permissions (`compute.addresses.create`, `compute.instances.update`).

### Procedure

1. Navigate to **VPC Network → External IP Addresses** in the Google Cloud Console.  
2. Click **Reserve static address**.
3. Provide a **name** for the static IP (e.g., `my-static-ip`).
4. Configure the following options:
   - **Network service tier:**  
     - *Premium* (default): global routing with optimal performance.  
     - *Standard*: regional routing, lower cost.
   - **IP version:**  
     - *IPv4* (default) or *IPv6*.
   - **Type:**  
     - *Regional* – used with zonal resources such as VM instances.  
     - *Global* – used with global resources such as HTTP(S) Load Balancers.
5. Click **Reserve** to allocate the static IP.

The reserved address appears in the list with the **Type** set to *Static*.

---

## Assigning a Static IP to a VM Instance

1. Go to **VPC Network → External IP Addresses**.  
2. Locate the reserved static IP and click **Change**.  
3. Select the target VM instance from the list.  
4. Confirm the change.  
5. The previously assigned ephemeral IP (if any) will be automatically released.

Once attached, the VM instance will use the reserved static IP for all external communication.

---

## Verification

To confirm the assignment:
1. Navigate to **Compute Engine → VM Instances**.  
2. Review the **External IP** column for the VM.  
3. Stop and start the VM to verify that the static IP remains unchanged.

---

## Notes

- Static IPs that are reserved but **not attached** to any resource may incur charges.  
- Static IPs can be reassigned to different resources within the same region.  
- Deleting a VM does **not** release its associated static IP automatically; the IP remains reserved until manually released.  
- All static IP management operations can also be performed using the `gcloud` CLI or REST API.

---

## Summary

| Attribute | Ephemeral IP | Static IP |
|------------|---------------|------------|
| Assignment | Automatic | Manual (reserved) |
| Persistence | Changes on restart | Fixed until released |
| Scope | Regional | Regional or Global |
| Cost | Free (while attached) | Charged when idle |
| Recommended for | Temporary instances | Production workloads |

---

## Related Topics

- [Reserving a Static External IP Address](https://cloud.google.com/compute/docs/ip-addresses/reserve-static-external-ip-address)  
- [Assigning, Releasing, and Managing IP Addresses](https://cloud.google.com/vpc/docs/using-vpc#ip-addresses)  
- [Load Balancers and Global Static IPs](https://cloud.google.com/load-balancing/docs/using-static-ip)

---
