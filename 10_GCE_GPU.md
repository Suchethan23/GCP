# 🎮 GPUs in Compute Engine

## 🔍 What Are GPUs?
GPUs (Graphics Processing Units) are specialized hardware accelerators for **math-intensive** and **graphics-intensive** workloads.  
They are widely used for:

- AI / Machine Learning  
- Deep Learning  
- Scientific computing  
- Rendering & visualization  

Adding a GPU to a VM can massively increase performance for these workloads.

---

## ⚡ Benefits of Adding a GPU
- High-speed parallel processing  
- Significant performance boost for ML/AI tasks  
- Faster training and inference workloads  
- Optimized for vectorized mathematical operations  

---

## 💡 Important Requirements
To use a GPU effectively:
- You **must use VM images with GPU drivers/libraries pre-installed**  
  (e.g., CUDA, NVIDIA drivers)
- Without proper GPU software, the GPU will **not** be utilized efficiently

---

## ❌ Restrictions & Limitations
- GPUs are **not supported** on all machine types  
  (e.g., **E2**, shared-core machines, memory-optimized types)
- **Live Migration is NOT supported** for GPU-attached VMs
  - `On-host maintenance` **must be set to: Terminate**
- Spot/Preemptible VMs with GPUs have limited availability
- GPU VMs typically cost more due to high-performance hardware

---

## 🛠️ Availability Policy Recommendations
For GPU-enabled VMs:
- **On-host maintenance:** `Terminate VM instance`  
  (required because live migration is not supported)
- **Automatic restart:** `ON`  
  Ensures VM restarts after maintenance or hardware failure

---

## 👇 How to Add GPUs to a VM

### **1. Choose a GPU Machine Family**
Google Cloud provides dedicated GPU families.  
Select the **GPU machine family** directly when creating the VM.

### **2. Add GPUs to an Existing Machine Family**
- Choose a supported machine family like **N1** or **N2**
- Scroll to **CPU & GPU** section
- Click **Add GPU**
- GPU options appear only for compatible machine types

Example:
- **E2** → GPU option disabled  
- **N1/N2** → GPU option available  

---

## 📝 Summary
- GPUs accelerate ML, AI, and graphics workloads.  
- Use an image with GPU drivers installed (CUDA/NVIDIA).  
- Not supported on all machine types; no live migration allowed.  
- Configure **Terminate** for on-host maintenance and **Automatic restart** to ON.  
- You can either pick a GPU machine family or add GPUs to supported families like **N1/N2**.

