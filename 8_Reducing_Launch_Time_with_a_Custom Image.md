# Reducing Launch Time with a Custom Image

## Overview
Virtual machine (VM) provisioning often involves executing startup scripts that install software and apply operating system (OS) patches.  
While effective, this approach increases the launch time of each VM because installations and updates occur during instance creation.

A more efficient approach is to use a **custom image** — a prebuilt image that includes the OS, software, configurations, and security updates.  
Instances created from this image start faster since no installation is needed at boot time.

---

## Concept
A **custom image** in Google Cloud is a reusable disk image that serves as the foundation for new VM instances.  
It can be created from several sources:

- A VM instance  
- A persistent disk  
- A snapshot  
- Another existing image  
- A file stored in Cloud Storage  

When a custom image is used, each new instance launches with identical configurations and preinstalled components, ensuring consistency and reducing boot-up delays.

---

## Image Creation Process
A custom image is typically derived from the persistent disk of a preconfigured VM instance.

### Key Considerations
- **The source instance must be stopped** before image creation.  
  Creating an image from an active instance may result in inconsistent data or errors.  
- **Storage location** can be regional or multi-regional.  
  Multi-regional storage is preferred when images will be used across multiple regions.

### Creation Steps (Conceptual)
1. Identify the VM instance whose disk will serve as the source.  
2. Stop the instance to ensure data integrity.  
3. From the **Disks** section in Compute Engine, select the disk and choose **Create Image**.  
4. Specify:
   - **Source**: The chosen disk  
   - **Name**: A descriptive image name (e.g., `my-custom-image`)  
   - **Location**: Regional or multi-regional  
   - **Encryption**: Default or custom as per policy  
5. The image appears under **Compute Engine → Images** once the creation process completes.

---

## Integration with Instance Templates
Custom images can be used directly within **Instance Templates** to standardize deployments.

By referencing a custom image in a template:
- Software installation steps are eliminated from startup scripts.
- Startup scripts can be minimized to simple configuration tasks, such as initializing services or writing configuration files.

### Example Minimal Startup Script
```bash
echo "<h1>Server Initialized</h1>" > /var/www/html/index.html
service apache2 start
```


## Security Hardening

Custom images are often used to enforce corporate or organizational security baselines.  
A **hardened image** includes:

- Latest OS and security patches  
- Pre-installed security agents and monitoring tools  
- Configured firewall and SSH rules  
- Disabled unnecessary services  

By deploying hardened images, all VM instances automatically comply with internal security standards without requiring manual setup at runtime.

---

## Image Lifecycle Management

Google Cloud allows active management of image versions through **deprecation** and **recommendation** policies.

### Deprecation Workflow

When an older image becomes outdated:

1. Mark the existing image as **deprecated**.  
2. Define a **recommended replacement image**.  

This ensures consistent migration to newer image versions and prevents the use of obsolete configurations.

**Example:**

- `base-image-v1` → *Deprecated*  
- `base-image-v2` → *Recommended replacement*  

Deprecation policies simplify maintenance and version control across environments.

---

## Advantages of Using Custom Images

| **Category** | **Benefit** |
|---------------|-------------|
| Launch Time | Eliminates installation overhead and reduces VM startup duration |
| Consistency | Ensures identical configuration across all instances |
| Security | Supports hardened, policy-compliant system baselines |
| Scalability | Enables faster provisioning for autoscaling groups |
| Maintainability | Simplifies lifecycle management with deprecation and replacement policies |

---

## Architectural Overview

The process of using a custom image in Compute Engine can be represented as follows:

    ┌────────────────────┐
    │   VM Instance      │
    │ (Configured +      │
    │  Software Installed)│
    └────────┬───────────┘
             │
             ▼
    ┌────────────────────┐
    │ Persistent Disk     │
    │ (OS + Apps)         │
    └────────┬───────────┘
             │
             ▼
    ┌────────────────────┐
    │ Custom Image        │
    │ (Reusable Baseline) │
    └────────┬───────────┘
             │
             ▼
    ┌────────────────────┐
    │ Instance Template   │
    │ (References Image)  │
    └────────┬───────────┘
             │
             ▼
    ┌────────────────────┐
    │ VM Instances        │
    │ (Launch Instantly)  │
    └────────────────────┘
