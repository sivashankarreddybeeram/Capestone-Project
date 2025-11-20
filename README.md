# 💾 NTFS vs. EXT4: A Comparative Study of Performance and Forensic Readiness

**Capstone Project | System Administration and Operating System Concepts**

[cite_start]_Team Members: Siva Shankar Reddy Beeram, Amanda Gwaba, Avipsa Sharma Paudel_ [cite: 205, 206, 207]

[cite_start]This project presents a comparative analysis of **NTFS** (New Technology File System) and **EXT4** (Fourth Extended File System) [cite: 216] [cite_start]on a USB 3.2 Gen 1 Flash Drive with Ubuntu 22.04 VM[cite: 216]. [cite_start]It covers read/write performance benchmarking and data recovery efficacy using the digital forensic tool **Autopsy**[cite: 217]. [cite_start]Our goal is to determine which file system offers superior speed, metadata retention, and effective file restoration for **forensic readiness** and **enterprise use**[cite: 218].

---

## 🌟 Project Highlights

* [cite_start]**Dual Focus:** Compares file systems from two critical perspectives: **Performance** (speed/latency) and **Forensic Readiness** (data recoverability and metadata preservation)[cite: 222].
* [cite_start]**Key Finding (Performance):** **EXT4** demonstrated approximately **ten times faster** average write performance compared to NTFS when both were mounted on a Linux host, primarily due to NTFS reliance on the slower FUSE layer[cite: 223].
* [cite_start]**Key Finding (Forensics):** **NTFS** proved superior for recovery, retaining filenames and path structure, while EXT4 often yielded generic "Orphan Files"[cite: 315].
* [cite_start]**Tooling:** Utilized native Linux utilities (`/usr/bin/time` and `cp`) for benchmarking and **Autopsy** for digital forensic analysis[cite: 225].

---

## 🎯 Objectives

[cite_start]The project addresses primary research questions and concludes with evidence-based recommendations[cite: 227]:

* **Compare NTFS and EXT4** in terms of:
    * [cite_start]Read/write performance across file types and workloads [cite: 229]
    * [cite_start]Data recovery capabilities for different deleted files [cite: 230]
    * [cite_start]Metadata preservation essential for forensic investigations [cite: 231]
* [cite_start]Evaluate which file system is advisable for **recovery readiness**[cite: 233].

### **Skills Developed**

* [cite_start]Digital forensic data acquisition [cite: 237]
* [cite_start]File system analysis (NTFS, EXT4) on Linux [cite: 238]
* [cite_start]Use of **Autopsy** for data recovery and validation [cite: 239]
* [cite_start]Generation and interpretation of forensic metrics [cite: 240]

---

## 🧪 Methodology & Test Environment

### [cite_start]**Test Setup** [cite: 241]

| Component | Specification | Source |
| :--- | :--- | :--- |
| **Hardware** | [cite_start]SanDisk USB 3.2 Gen 1 Flash Drive, 125 GB [cite: 243] [cite_start]| [cite: 243] |
| **Host/Software** | [cite_start]Ubuntu 22.04 (VirtualBox VM) [cite: 245] [cite_start]| [cite: 245] |
| **Benchmark Tools** | [cite_start]`/usr/bin/time` and `cp` [cite: 246] [cite_start]| [cite: 246] |
| **Forensic recovery** | [cite_start]Autopsy (latest Linux release) [cite: 247] [cite_start]| [cite: 247] |

### [cite_start]**Data Files Used** [cite: 248]

[cite_start]A diverse set of files was selected for realistic benchmarking and recovery scenarios[cite: 249]:

| File Name | Type | Description |
| :--- | :--- | :--- |
| `audio.mp3` | Audio | [cite_start]Medium-size media file [cite: 250] |
| `data.zip` | ZIP Archive | [cite_start]Compressed dataset [cite: 250] |
| `video1.mp4`, `video2.mp4` | MP4 Video | [cite_start]Large media files [cite: 250] |
| `document.pdf` | PDF Document | [cite_start]Final reports & documentation [cite: 250] |
| `chrome.deb` | Installation Package | [cite_start]Application installer [cite: 250] |

### [cite_start]**Methodology Snippets** [cite: 257]

| File System | Action | Command |
| :--- | :--- | :--- |
| **NTFS Setup** | Format partition | [cite_start]`sudo mkfs.ntfs -f /dev/sdb1` [cite: 260] |
| **EXT4 Setup** | Format partition | [cite_start]`sudo mkfs.ext4 -f /dev/sdb1` [cite: 263] |
| **Mounting** | Attach partition for testing | [cite_start]`sudo mount /dev/sdb1 /mnt/usb` [cite: 261, 264] |
| **Benchmarking**| Record elapsed time for copying | [cite_start]`/usr/bin/time -f "%E" cp <file> /mnt/usb` [cite: 266] |

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

[cite_start]For environments that prioritize **performance and low write latency** (especially for handling large files) on a Linux host, the **EXT4 file system is demonstrably superior** due to its native kernel support[cite: 309]. [cite_start]Overall, EXT4 demonstrated approximately **45–60% higher efficiency** than NTFS in this experiment[cite: 311].

### [cite_start]**Recommendation** [cite: 312]

* [cite_start]**For Performance (Linux-Only):** Use **EXT4**[cite: 313].
* [cite_start]**For Cross-Platform Compatibility:** Use **NTFS** but be aware of the **severe write latency penalty** when operating in a Linux environment[cite: 314].
* [cite_start]**For Forensic Scenarios:** **NTFS is generally preferred for data recoverability** as it retains filenames and path structure, while **EXT4 recovery is faster** but often yields generic orphan files, requiring more manual effort to identify[cite: 315].

### [cite_start]**Limitations** [cite: 316]

* [cite_start]NTFS suffers serious write bottleneck under Linux due to FUSE driver overhead[cite: 317].
* [cite_start]EXT4 recovery yields orphan files after deletion, losing original folder/filename[cite: 318].
* [cite_start]USB hardware speed caps maximum performance for both systems[cite: 319].

---

## 🔗 Project Links and Reports

| Report Title | GitHub Link |
| :--- | :--- |
| **Overall Final Report** | [cite_start][Link to Final Report] [cite: 320] |
| **NTFS VS EXT4 Benchmarking Report** | [cite_start][Link to Benchmarking Report] [cite: 321] |
| **Autopsy Report (Data Recovery - NTFS)** | [cite_start][Link to NTFS Autopsy Report] [cite: 322] |
| **Autopsy Report (Data Recovery - EXT4)** | [cite_start][Link to EXT4 Autopsy Report] [cite: 323] |
