# 💾 NTFS vs. EXT4: A Comparative Study of Performance and Forensic Readiness

**Capstone Project | System Administration and Operating System Concepts**

Team Members: Siva Shankar Reddy Beeram, Amanda Gwaba, Avipsa Sharma Paudel

This project presents a comparative analysis of **NTFS** (New Technology File System) and **EXT4** (Fourth Extended File System) on a USB 3.2 Gen 1 Flash Drive with Ubuntu 22.04 VM. It covers read/write performance benchmarking and data recovery efficacy using the digital forensic tool **Autopsy**. Our goal is to determine which file system offers superior speed, metadata retention, and effective file restoration for **forensic readiness** and **enterprise use**.

USB drives are ubiquitous in incident response, malware forensics, and regulatory audits. Knowing how file systems respond to deletion and recovery operations prepares professionals for high-stakes investigations.

#### Target Audience and Relevance

This project is intended for digital forensics practitioners, system administrators, pen-testers, and cybersecurity students interested in file system benchmarking and practical data recovery.

---

## 🌟 Project Highlights

* **Dual Focus:** Compares file systems from two critical perspectives: **Performance** (speed/latency) and **Forensic Readiness** (data recoverability and metadata preservation).
* **Key Finding (Performance):** **EXT4** demonstrated approximately **ten times faster** average write performance compared to NTFS when both were mounted on a Linux host, primarily due to NTFS reliance on the slower FUSE layer.
* **Key Finding (Forensics):** **NTFS** proved superior for recovery, retaining filenames and path structure, while EXT4 often yielded generic "Orphan Files".
* **Tooling:** Utilized native Linux utilities (`/usr/bin/time` and `cp`) for benchmarking and **Autopsy** for digital forensic analysis.

---

## 🎯 Objectives

The project addresses primary research questions and concludes with evidence-based recommendations:

* **Compare NTFS and EXT4** in terms of:
    * Read/write performance across file types and workloads
    * Data recovery capabilities for different deleted files
    * Metadata preservation essential for forensic investigations
* Benchmark using reliable, repeatable Linux methods.
* Evaluate which file system is advisable for **recovery readiness**.

### **Skills Developed**

* Digital forensic data acquisition
* File system analysis (NTFS, EXT4) on Linux
* Use of **Autopsy** for data recovery and validation
* Generation and interpretation of forensic metrics

---

## 🧪 Methodology & Test Environment

### **Test Environment**

**Hardware**
* SanDisk USB 3.2 Gen 1 Flash Drive, 125 GB

**Host/Software** - Ubuntu 22.04 (VirtualBox VM)

**Benchmark Tools** - `/usr/bin/time` and `cp`

**Forensic recovery** - Autopsy (4.22.1)

### **Data Files Used**

A diverse set of files was selected for realistic benchmarking and recovery scenarios:

| File Name | Type | Description |
| :--- | :--- | :--- |
| `audio.mp3` | Audio | Medium-size media file |
| `data.zip` | ZIP Archive | Compressed dataset |
| `video1.mp4`, `video2.mp4` | MP4 Video | Large media files |
| `document.pdf` | PDF Document | Final reports & documentation |
| `chrome.deb` | Installation Package | Application installer |

### Usage/Replication Instructions

To reproduce these benchmarks and recovery steps:

* Prepare a USB flash drive; format using NTFS and EXT4 as shown in the methodology.
* Use provided Linux commands to benchmark read/write speeds.
* Delete the test files, then perform recovery with Autopsy.
* Compare your timing and results with the tables and charts provided here.

### **Methodology**

**File System Setup**
* NTFS
 * Format with sudo mkfs.ntfs -f /dev/sdb1
 * Mount for testing: sudo mount /dev/sdb1 /mnt/usb
* EXT4
  * Format with sudo mkfs.ext4 -f /dev/sdb1
  * Mount for testing: sudo mount /dev/sdb1 /mnt/usb

**Benchmarking**

* Write: cp <file> /mnt/usb (record wall-clock elapsed time)
* Read: cp /mnt/usb/<file> <destination> (record wall-clock elapsed time)

**Data Recovery**

* Files deleted manually after copying.
* USB scanned using Autopsy:
  * Case setup, data source addition
  * Modules: File Type Identification, Carve Files
  * Recovered deleted files recorded, metadata checked

---

## 📈 Performance Benchmarking

### [cite_start]**Raw Performance Data (Elapsed Time in Seconds)** [cite: 274, 275, 278]

| File | NTFS Write (s) | EXT4 Write (s) | NTFS Read (s) | EXT4 Read (s) |
| :--- | :--- | :--- | :--- | :--- |
| `audio.mp3` | 0.02 | 0.02 | 0.01 | 0.01 |
| `data.zip` | **1.18** | 0.00 | 0.04 | 0.01 |
| `video1.mp4`| 0.83 | 0.05 | 0.03 | 0.07 |
| `chrome.deb`| 0.07 | 0.08 | — | **0.14** |
| **AVERAGE** | **0.31s** | **0.03s** | **0.03s** | **0.04s** |

### **Write and Read Speed Comparison: NTFS vs EXT4**

[cite_start]The bar chart visually highlights how **EXT4 consistently outperforms NTFS in write speeds** across almost all file types, with read speeds nearly equal except for minor variations[cite: 282].



### [cite_start]**Key Performance Metrics** [cite: 284, 285]

| Metric | Best Performer | Rationale |
| :--- | :--- | :--- |
| **Overall Write Speed** | **EXT4 (~10x faster)** | [cite_start]~10x faster average due to native kernel support[cite: 285]. |
| **Overall Read Speed** | **Near Parity** | [cite_start]USB hardware is a bottleneck, NTFS showed slightly lower average latency[cite: 285]. |
| **Large File Handling** | **EXT4** | [cite_start]Instantaneous writes for `.zip`, `.mp4` vs. seconds for NTFS[cite: 285]. |

---

## 🔎 Data Recovery Summary (Using Autopsy)

[cite_start]The data recovery phase focused on comparing the forensic readiness of both file systems after files were intentionally deleted[cite: 289].

### [cite_start]**Forensic Process** [cite: 300]

1.  [cite_start]A new case was created in Autopsy for each file system (NTFS and EXT4)[cite: 301].
2.  [cite_start]The USB drive was added as a local disk data source[cite: 302].
3.  [cite_start]Ingest modules like **"File Type Identification"** and **"Carve Files"** were enabled to ensure maximum recovery potential[cite: 303].

### [cite_start]**Key Recovery Observations** [cite: 304]

| File System | Deleted Files Located | Recovery Observations |
| :--- | :--- | :--- |
| **NTFS** | [cite_start]Files identified by name (e.g., `chrome.deb`, `data.zip`)[cite: 305]. | [cite_start]**Successful.** Deleted file scan shows comprehensive file restoration (normal filenames and folder structure retained)[cite: 292]. |
| **EXT4** | [cite_start]Files appeared as generic **"Orphan Files"**[cite: 306]. | [cite_start]**Partial/Unsuccessful.** Extracted files were labeled with numerical identifiers and shown as **0 KB** in size, indicating data blocks were not fully recoverable or correctly reassembled[cite: 307]. |

---

## 🎓 Conclusion, Recommendation & Limitations

For environments that prioritize **performance and low write latency** (especially for handling large files) on a Linux host, the **EXT4 file system is demonstrably superior** due to its native kernel support. While NTFS is necessary for cross-platform compatibility with Windows, EXT4 provides better efficiency, lower latency, and superior throughput for Linux-native operations. Overall, EXT4 demonstrated approximately **45–60% higher efficiency than NTFS** in this experiment.

### **Recommendation**

* **For Performance (Linux-Only):** Use **EXT4**.
* **For Cross-Platform Compatibility:** Use **NTFS** but be aware of the **severe write latency penalty** when operating in a Linux environment.
* **For Forensic Scenarios:** **NTFS is generally preferred for data recoverability** as it retains filenames and path structure, while **EXT4 recovery is faster** but often yields generic orphan files, requiring more manual effort to identify.

### **Limitations**

* NTFS suffers serious write bottleneck under Linux due to FUSE driver overhead.
* EXT4 recovery yields orphan files after deletion, losing original folder/filename.
* USB hardware speed caps maximum performance for both systems.

---

## 🔗 Project Links and Reports

**Overall Final Report** - https://github.com/sivashankarreddybeeram/Capestone-Project/blob/7e23ea940b59cc023eab283c74899c4f40bcfd4c/Final%20Report.pdf

**NTFS VS EXT4 Benchmarking Report** - https://github.com/sivashankarreddybeeram/Capestone-Project/blob/7e23ea940b59cc023eab283c74899c4f40bcfd4c/NTFS%20VS%20EXT4%20Benchmarking%20Report.pdf

**Autopsy Report (Data Recovery - NTFS)** - https://github.com/sivashankarreddybeeram/Capestone-Project/blob/7e23ea940b59cc023eab283c74899c4f40bcfd4c/Autopsy%20Report%20(Data%20Recovery%20-%20NTFS).pdf

**Autopsy Report (Data Recovery - EXT4)** - https://github.com/sivashankarreddybeeram/Capestone-Project/blob/7e23ea940b59cc023eab283c74899c4f40bcfd4c/Autopsy%20Report%20(Data%20Recovery%20-%20EXT4).pdf
