# ☁️ GCP Cost Optimization — Sustained Use Discounts (SUD)

Keeping costs low is a major part of managing infrastructure on Google Cloud. One of the most effective automatic cost-saving mechanisms is **Sustained Use Discounts (SUDs)**.

---

## 🔍 What are Sustained Use Discounts?

**Sustained Use Discounts (SUDs)** are **automatic monthly discounts** applied when VM instances run for a significant portion of a billing month.

### ✔️ Key Characteristics
- **Automatic** — No manual configuration needed.
- **Discount increases with higher usage** of the VM within the same billing month.
- **Applied per VM**, per project, per region.

---

## 📊 How Sustained Use Discounts Work

### ➤ Eligibility Threshold
- If an **N1** or **N2** VM runs for **more than 25%** of the month, SUDs start applying.

### ➤ Discount Progression
- Discounts range from **20% to 50%**.
- Example:
  - Running **40%** of the month → smaller discount.
  - Running **80%** of the month → much higher discount.

### ➤ Automatic Application
- No action is needed from your side.
- Discounts are automatically added during billing.

---

## 💡 Where SUDs Apply

### ✔️ Applicable To:
- **Compute Engine** VMs (N1, N2 machine families)
- **Google Kubernetes Engine (GKE)** nodes  
  - Whether created manually or automatically by GKE.

---

## ❌ Where SUDs Do *Not* Apply

| Service / Machine Type | SUD Applies? | Notes |
|-------------------------|--------------|-------|
| **E2 machine types** | ❌ No | E2 has its own optimized pricing model. |
| **A2 machine types** | ❌ No | GPU-focused machines; no SUDs. |
| **App Engine Flexible** | ❌ No | Uses its own pricing model. |
| **Dataflow workers** | ❌ No | Dataflow has separate pricing; no VM SUDs. |

---

## 🧠 Additional Relevant Information (Not in Video But Important)

### 🔸 SUD vs Committed Use Discount (CUD)

| Feature | SUD | CUD |
|--------|-----|-----|
| Applied Automatically | ✔️ | ❌ Must be purchased |
| Based on Usage Hours | ✔️ | ❌ Based on the commitment |
| Discount Range | ~20–50% | Up to 57–70% |
| Best For | Unpredictable or variable workloads | Stable, predictable workloads |

### 🔸 Break-Even Logic
- If VM usage is **>70% of the month**, CUDs usually provide better savings than SUDs.

### 🔸 Per-Region Calculation
- Usage **does not combine across regions**.
- Discounts apply only within the same project + region + VM family.

---

## 📝 Summary

- Sustained Use Discounts = **automatic VM cost savings**.
- Applied when N1/N2 VMs run **>25% of the month**.
- Discounts grow up to **50%** with more usage.
- Works for **Compute Engine** and **GKE** node VMs.
- **Not applicable** for E2, A2, App Engine Flex, or Dataflow-created VMs.

---

# 💰 Committed Use Discounts (CUD) — GCP

## 🔍 What Are CUDs?
Committed Use Discounts provide **large cost reductions** when you commit to using specific Compute Engine resources for **1 or 3 years**.

- Requires **commitment** → not automatic.
- Discounts up to **70%** (higher than Sustained Use Discounts).
- Best for **predictable, long-running workloads**.

---

## ✔️ Where CUDs Apply
- **Compute Engine** VMs  
- **Google Kubernetes Engine (GKE)** node VMs

Automatically applied to matching VM instances after purchase.

---

## ❌ Where CUDs Do NOT Apply
- **App Engine Flexible**
- **Dataflow worker VMs**

---

## 🛠️ How to Purchase
1. Go to **Compute Engine → Committed Use Discounts**
2. Click **Purchase Commitment**
3. Select:
   - Region  
   - Machine family  
   - vCPUs, memory, GPUs, local SSD  
   - Duration (1 or 3 years)
4. Confirm purchase

---

## 📝 Summary
- CUDs = best savings for stable workloads.
- Higher savings than SUDs.
- Requires upfront commitment and cannot be cancelled.
- Ideal for workloads like long-running web apps, APIs, and stable GKE clusters.

# ⚡ Preemptible Virtual Machines (GCP)

## 🔍 What Are Preemptible VMs?
Preemptible VMs are **short-lived, low-cost Compute Engine instances**.  
They are similar to **AWS Spot Instances**.

- Maximum runtime: **24 hours**
- Can be terminated **anytime within 24 hours**
- You get a **30-second termination warning**

---

## 💰 When to Use Preemptible VMs
Use them only when:
- Workloads are **fault-tolerant**
- You can **stop/start anytime**
- You need **very low-cost compute**
- Workloads are **not time-critical**

### Good examples:
- Batch jobs  
- Data processing  
- Rendering  
- Non-immediate workloads

---

## ❌ Restrictions
- **Not guaranteed** to be available
- **No SLA** from Google Cloud
- Cannot be **converted** to a regular VM
- Cannot be **auto-restarted**
- **Free-tier credits do NOT apply**
- Should not be used for production or user-facing apps

---

## 🛠️ How to Enable Preemptible VM
1. Go to **Compute Engine → VM Instances → Create**
2. Open **Management → Availability Policy**
3. Toggle **Preemptibility = On**

---

## 📝 Summary
- Preemptible VMs = **very cheap but short-lived** compute.
- Ideal for **non-urgent, fault-tolerant batch workloads**.
- Terminated anytime; maximum life is 24 hours.

# ⚡ Spot VMs (GCP)

## 🔍 What Are Spot VMs?
Spot VMs are the **newer version of Preemptible VMs** in Google Cloud.  
They offer **very low-cost compute** but can be terminated at any time.

---

## 🔑 Key Difference from Preemptible VMs
| Feature | Preemptible VMs | Spot VMs |
|---------|------------------|----------|
| Maximum runtime | **24 hours** | **No runtime limit** |
| Termination notice | 30 seconds | 30 seconds |
| Pricing | Discounted | **Dynamic pricing** (60–91% off) |

---

## ✔️ Features of Spot VMs
- No minimum or maximum runtime.
- Can be **reclaimed anytime** when GCP needs capacity.
- **30-second shutdown warning** (same as preemptible).
- **Very high discounts**: ~60%–91% cheaper than on-demand VMs.
- Might not always be available.
- **Free-tier credits cannot be used**.

---

## 📝 Summary
Spot VMs = Preemptible VMs **without the 24-hour limit**.  
They are ideal for:
- Batch processing  
- Fault-tolerant workloads  
- Cost-sensitive compute tasks  

But **not suitable** for production or user-facing systems due to sudden termination.

