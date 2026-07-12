# Mac-like Boot

This is to achieve mac-like boot up time (practically less than 5 sec).

**The HOW**: macOS features an incredibly low-power sleep state.
**The WHY**: Apple Silicon chips are so energy-efficient that when you close
the lid, the Mac suspends its state to RAM while consuming almost zero battery.
When you open the lid, it doesn't boot, it simply wakes up in a fraction of a sec.

### TL;DR

MacBooks boot so fast because Apple designs the chip, the storage,
the security protocol, and the operating system together.
Because the software knows exactly what hardware to expect,
it skips the "introductions" and goes straight to loading the desktop.

### Reasoning

1. Unified Architecture and NVMe storage
2. Boot ROM and Secure Enclave Integration
3. macOS Kernel Optimization
4. Hardware-Accelerated Decomposition
5. The "Fake" Boot(Sleep Mode with almost no battery drain instead of cold start)

### Goal
To achieve the same level of boot up speeds and fast forwards straight to
the login screen, just like mac.

### Step-by-step Blueprint by Gemini

1. Motherboard Tweaks (Shaving off "Firmware Time")
2. Switch to `systemd-boot` and Hide the Menu
3. Silent Boot & Tweak Kernel Parameters
4. Swap `mkinitcpio` or `dracut` for booster
5. Kill the Biggest Bottleneck (`NetworkManager-wait-online`)

### Changes I made to the system

1. Changed/Minimized `timeout` for `limine-boot` screen from 5 sec to 1 sec, reducing wait time
to choose the default kernel/snapshot. Learnt that its there's default option and
also remembers the last entry.
```bash
    $ sudo vim /boot/limine.conf

    # ...edit the timeout to set to 1, exit vim
```

2. Backed up the `/etc/default/limine` as `limine.bak.10_07_26`.
Updated KERNEL_CMDLINE with the below snippet resulted in disabling the plymouth splash.
```
KERNEL_CMDLINE[default]+="rootflags=subvol=/@ rd.luks.uuid=5cacd618-5ba6-428d-86b8-7e997b858e73 root=/dev/mapper/luks-5cacd618-5ba6-428d-86b8-7e997b858e73 quiet rd.udev.log_priority=3"
```

Then regenerate the limine config with running the command below-
```bash
$ limine-mkinitcpio
```

3. Disabled the `NetworkManager-wait-online`
```bash
    $ sudo systemctl disable NetworkManager-wait-online.service
```

4. Turned on the SDDM auto-login as I'm the sole user of my machine.

After all these, it almost booted around ~16 seconds on first reboot.
