# Lab Assignment 5 — PCS221 Cloud Computing (Microsoft Azure)
## VM Migration & Replication with Azure Site Recovery

---

## 📁 Repository Structure

```
lab5-repo/
├── ip.txt                          # Public IP of the migrated VM
├── README.md                       # This file — full documentation
└── screenshots/
    ├── 01_webpage_before_migration.png     # Apache webpage on original VM
    ├── 02_replication_enabled.png          # ASR replication status
    ├── 03_vm_status_protected.png          # VM shows "Protected" status
    ├── 04_test_failover_initiated.png      # Test Failover in progress
    ├── 05_test_failover_vm.png             # Test Failover VM running
    ├── 06_test_vm_apache_running.png       # Apache service on test VM
    ├── 07_test_vm_webpage.png              # Webpage on test VM via public IP
    ├── 08_cleanup_test_failover.png        # Cleanup Test Failover completed
    ├── 09_actual_failover_initiated.png    # Actual Failover in progress
    ├── 10_migrated_vm.png                  # Migrated VM running in target region
    ├── 11_migrated_vm_apache_running.png   # Apache service on migrated VM
    └── 12_migrated_vm_webpage.png          # Webpage on migrated VM via public IP
```

---

## 🌐 Public IP

The public IP of the migrated VM is stored in [`ip.txt`](./ip.txt).

---

## Q1 — Create VM & Configure Azure Site Recovery

### Step 1: Create / Use Existing Ubuntu VM (from Lab 4)

The original VM was created on **Microsoft Azure** in the **East US** region with:
- **OS:** Ubuntu 22.04 LTS
- **Size:** Standard B1s (or as configured in Lab 4)
- **Apache Web Server** installed and running
- **Port 80** open via Network Security Group (NSG)

**Apache Setup Commands (run on VM):**
```bash
sudo apt update
sudo apt install apache2 -y
sudo systemctl start apache2
sudo systemctl enable apache2
```

---

### Step 2: Create a Recovery Services Vault

1. Go to **Azure Portal** → Search `Recovery Services Vaults` → **+ Create**
2. Fill in:
   - **Subscription:** Your subscription
   - **Resource Group:** Create new or use existing (e.g., `lab5-asr-rg`)
   - **Vault Name:** e.g., `lab5-recovery-vault`
   - **Region:** Choose a **different region** from the source VM (e.g., West US)
3. Click **Review + Create** → **Create**

---

### Step 3: Enable Replication via Azure Site Recovery

1. Open the Recovery Services Vault → Click **Site Recovery** → **Enable Replication**

2. **Source Configuration:**
   - **Source location:** East US (where original VM is located)
   - **Azure Virtual Machine deployment model:** Resource Manager

3. **Select Virtual Machine:**
   - Choose your Ubuntu VM

4. **Target Configuration:**
   | Setting | Value |
   |---|---|
   | Target location | West US (or another region) |
   | Target resource group | `lab5-target-rg` (auto-created or custom) |
   | Target virtual network | Auto-created or custom VNet |
   | Cache storage account | Auto-created |
   | Replica managed disks | Auto-configured |

5. Click **Enable Replication**

6. Wait until the VM status shows **Protected** (usually takes 15–30 minutes)

> 📸 Screenshot: `03_vm_status_protected.png`

---

## Q2 — Perform Test Failover

### Step 1: Initiate Test Failover

1. In the Recovery Services Vault → **Replicated Items** → Select your VM
2. Click **Test Failover**
3. Configure:
   - **Recovery Point:** Latest (lowest RPO)
   - **Azure Virtual Network:** Select the target test VNet

4. Click **OK** — Azure creates a test VM in the target region

> 📸 Screenshot: `04_test_failover_initiated.png`

---

### Step 2: Verify Test Failover VM

Once the test failover VM is running:

1. Go to the test VM → Copy its **Public IP Address**
2. SSH into the test VM:
   ```bash
   ssh azureuser@<test-vm-public-ip>
   ```
3. Check Apache service status:
   ```bash
   sudo systemctl status apache2
   ```
   Expected output: `active (running)` ✅

4. Open a browser and navigate to `http://<test-vm-public-ip>` to confirm the Apache webpage is accessible ✅

> 📸 Screenshots: `05_test_failover_vm.png`, `06_test_vm_apache_running.png`, `07_test_vm_webpage.png`

---

### Step 3: Cleanup Test Failover

1. Go back to the replicated item → Click **Cleanup Test Failover**
2. Add notes (optional): `"Test verified successfully — Apache running and webpage accessible"`
3. Check **Testing is complete** → Click **OK**

Azure deletes the test VM and cleans up associated resources.

> 📸 Screenshot: `08_cleanup_test_failover.png`

---

## Q3 — Perform Actual VM Migration (Failover)

### Step 1: Initiate Failover

1. In the Recovery Services Vault → **Replicated Items** → Select your VM
2. Click **Failover**
3. Configure:
   - **Recovery Point:** Latest (lowest RPO)
   - Check **Shut down machine before beginning failover** (optional but recommended for data consistency)
4. Click **OK**

> 📸 Screenshot: `09_actual_failover_initiated.png`

---

### Step 2: Commit the Migration

1. Once failover completes, click **Commit**
2. Confirm by clicking **OK**

This finalizes the migration — the VM is now permanently running in the target region.

---

### Step 3: Verify Migrated VM

1. Navigate to **Virtual Machines** in Azure Portal → Find the migrated VM in the target region
2. Copy its **Public IP Address** → update `ip.txt`
3. SSH into the migrated VM:
   ```bash
   ssh azureuser@<migrated-vm-public-ip>
   ```
4. Verify Apache is running:
   ```bash
   sudo systemctl status apache2
   ```
   Expected: `active (running)` ✅

5. Open a browser → `http://<migrated-vm-public-ip>` → Confirm webpage is accessible ✅

6. Verify data consistency:
   ```bash
   ls /var/www/html/
   cat /var/www/html/index.html
   ```

> 📸 Screenshots: `10_migrated_vm.png`, `11_migrated_vm_apache_running.png`, `12_migrated_vm_webpage.png`

---

## ✅ Summary

| Task | Status |
|---|---|
| Ubuntu VM with Apache created | ✅ |
| Recovery Services Vault created in different region | ✅ |
| Replication enabled via Azure Site Recovery | ✅ |
| VM status shows Protected | ✅ |
| Test Failover initiated and verified | ✅ |
| Test Failover cleanup completed | ✅ |
| Actual Failover (Migration) performed | ✅ |
| Migration committed | ✅ |
| Apache running on migrated VM | ✅ |
| Webpage accessible on migrated VM | ✅ |
| Data consistency verified | ✅ |

---

## 📝 Notes

- The original VM was **not shut down** during the lab (as per assignment instructions) to keep the webpage accessible for evaluation.
- Azure Site Recovery replicates the VM asynchronously; the **RPO (Recovery Point Objective)** depends on replication lag.
- All screenshots are available in the `/screenshots` folder.
