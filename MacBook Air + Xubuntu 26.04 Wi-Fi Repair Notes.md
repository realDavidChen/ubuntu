# MacBook Air + Xubuntu 26.04 Wi-Fi Repair Notes

## Symptom

After installing Xubuntu 26.04 successfully:

* No Wi-Fi icon
* "No network devices available"
* Bluetooth works normally
* Network card hardware is detected

## Diagnosis

Check the wireless chip:

```bash
lspci | grep -i network
```

Result:

```text
Broadcom BCM4360
```

Check the loaded driver:

```bash
lspci -nnk | grep -A3 -i network
```

Result shows:

```text
Kernel driver in use: bcma-pci-bridge
```

Check modules:

```bash
lsmod | grep -E 'b43|bcma|wl'
```

Result:

```text
b43
bcma
```

Check wl driver:

```bash
modinfo wl
```

Result:

```text
Module wl not found
```

Conclusion:

The Wi-Fi hardware is healthy.

The system loaded the wrong Broadcom driver (b43/bcma).

The correct Broadcom STA driver (wl) is missing.

---

## Solution

### Step 1

Use Android USB tethering.

Connect phone via USB.

Enable:

```text
USB Tethering
```

Verify network:

```bash
ping google.com
```

---

### Step 2

Update package list:

```bash
sudo apt update
```

---

### Step 3

Install Broadcom STA driver:

```bash
sudo apt install broadcom-sta-dkms
```

Wait for:

```text
Building module(s)... done
Installing ... wl.ko
```

---

### Step 4

Reboot:

```bash
sudo reboot
```

---

## Verification

Check:

```bash
lsmod | grep wl
```

or

```bash
lspci -nnk | grep -A3 -i network
```

Expected result:

```text
Kernel driver in use: wl
```

Wi-Fi networks should appear normally.

---

## Key Lesson

Do NOT immediately reinstall Xubuntu.

For BCM4360 on old MacBook Air models:

The hardware is usually fine.

The problem is usually a missing Broadcom STA driver.

Installing:

```bash
sudo apt install broadcom-sta-dkms
```

is often the complete fix.
