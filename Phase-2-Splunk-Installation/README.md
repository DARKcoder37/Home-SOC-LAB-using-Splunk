# Phase 2 — Splunk Enterprise Installation

## Objective

Prepare the Ubuntu Desktop virtual machine for Splunk Enterprise by verifying the installed operating system, checking available storage, and confirming that the system is ready for installation.

## Ubuntu VM requirements

| Component | Configuration |
|---|---|
| VM Role | Ubuntu Desktop — Splunk Server |
| Operating System | Ubuntu 22.04.5 LTS |
| Architecture | x86-64 |
| Allocated Size | 40 GiB |
| Lab IP Address | `192.168.50.30` |

## Network Architecture

The Ubuntu Desktop VM is intended to use two network adapters:

- **Adapter 1 — Internal Network (`SOC-LAB`):** Used for communication with other virtual machines in the isolated SOC lab.

![SOC Home Lab Network Architecture](screenshots/phase1-network-architecture.png)

*Figure 1: Ubuntu adapter 1 setting*
  
- **Adapter 2 — NAT:** Used to access the internet for downloading packages and installation files.

![SOC Home Lab Network Architecture](screenshots/phase1-network-architecture.png)

*Figure 2: Ubuntu adapter 2 setting*

> Enable or disable the network adapters as required. Use **Adapter 1 (Internal Network — `SOC-LAB`)** for communication between lab VMs and **Adapter 2 (NAT)** for internet connectivity. Enable only the adapter needed for the current task and disable the other adapter when it is not required.

## Configuration and Validation

### Step 1: Verify the Ubuntu Version

Open the terminal in Ubuntu Desktop and run:

```bash
cat /etc/os-release
```

Alternatively, use:

```bash
lsb_release -a
```

These commands display the installed Ubuntu release and version information.

**Screenshot:** [View Ubuntu Version](./screenshots/ubuntu-version.png)

### Step 2: Check Available Storage

Run the following command:

```bash
df -h
```

This displays filesystem capacity, used space, available space, and mount points in a human-readable format.

To check the filesystem containing the root directory specifically, run:

```bash
df -h /
```

Review the `Size`, `Used`, and `Avail` columns to determine how much space is available before installing Splunk Enterprise.

**Screenshot:** [View Ubuntu Storage](./screenshots/ubuntu-storage.png)

### Step 3: Check the Disk Layout

Run:

```bash
lsblk
```

This command lists detected block devices, disks, partitions, and their mount points. Use it alongside `df -h` to understand the storage available to the operating system.

**Screenshot:** [View Ubuntu Disk Layout](./screenshots/ubuntu-disk-layout.png)

### Step 4: Review Splunk Enterprise Storage Requirements

The storage required for Splunk Enterprise depends on the selected release, installation files, indexed log volume, and data-retention period.

For this home lab, **20 GB of free space is a practical starting estimate** for installation and basic testing. It is not a guaranteed official minimum, and more space may be needed as logs are collected and indexed.

Before installation:

1. Check the available space using `df -h`.
2. Check the disk layout using `lsblk`.
3. Review the system requirements for the specific Splunk Enterprise release being installed.

Official documentation:

- [Splunk Enterprise Documentation](https://docs.splunk.com/Documentation/Splunk)
- [Splunk Enterprise Installation Manual](https://docs.splunk.com/Documentation/Splunk/latest/Installation)

## Security Considerations

- Download Splunk Enterprise from the official Splunk website.
- Keep the lab network isolated from untrusted networks.
- Monitor available storage as indexed log data increases.
- Use the SOC lab for authorized security monitoring and testing.

## Results

This phase documents the preliminary checks required before installing Splunk Enterprise.

- Ubuntu version can be verified through the terminal.
- Available filesystem space can be checked using `df -h`.
- Disk devices and partitions can be inspected using `lsblk`.
- Storage readiness can be assessed against the requirements of the selected Splunk release.

**Status:** Splunk Enterprise installation and service validation must be documented after they have been completed and verified.

## Evidence

The following screenshots should be saved in the `screenshots` directory within the Phase 2 folder.

| Screenshot | Purpose |
|---|---|
| [ubuntu-version.png](./screenshots/ubuntu-version.png) | Shows the installed Ubuntu version |
| [ubuntu-storage.png](./screenshots/ubuntu-storage.png) | Shows filesystem capacity and available space |
| [ubuntu-disk-layout.png](./screenshots/ubuntu-disk-layout.png) | Shows detected disks and partitions |

## References

- [Splunk Enterprise Documentation](https://docs.splunk.com/Documentation/Splunk)
- [Splunk Enterprise Installation Manual](https://docs.splunk.com/Documentation/Splunk/latest/Installation)
- [Ubuntu Documentation](https://help.ubuntu.com/)
