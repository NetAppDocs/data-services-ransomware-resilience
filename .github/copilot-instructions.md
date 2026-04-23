# Copilot Instructions for NetApp Ransomware Resilience documentation

## Repository overview

**Product:** NetApp Ransomware Resilience

This repository documents NetApp Ransomware Resilience, a data protection service that helps organizations detect, respond to, and recover from ransomware attacks. The service operates at the data security layer and provides protection for file shares and VM datastores across on-premises ONTAP, Cloud Volumes ONTAP, Azure NetApp Files, and Amazon FSx for NetApp ONTAP environments. Ransomware Resilience integrates with NetApp Console and leverages NetApp Backup and Recovery for comprehensive ransomware protection.

## Repository structure

* Root directory - .adoc and .yml that contain the documentation, sidebar, and landing page structure of the repository.
* `_include` - Reusable text blocks referenced in .adoc files in the root. 
* `media` - Images and diagrams that are elements of articles in the root directory. This includes .png and source files. 
* `_whatsnew` - Release notes in .adoc form that are aggregated in the whats-new.adoc file.
* `redirect` - .adoc files for retired pages and endpoints that redirect HTTPS requests to the appropriate endpoint.
* `support` - Support-related documentation pages including help and support registration tasks.

## Product-specific context

* **System** - a managed environment tied to a Console agent. Systems contain workloads. 
* **Workload** - logical groupings of resources that belong to a system, such as a file share.
 Volumes or databases that have been discovered by Ransomware Resilience through a recognized Console agent. Workloads can be discovered automatically and grouped for collective protection.
* **Protection strategy** - Comprehensive protection framework that encompasses detection policies, protection policies (snapshots and backups), and optional replication policies. Predefined strategies include Critical, Important, Standard, Encryption user extension, and Critical replication policies.
* **Clean restore** - Guided multi-step recovery process that uses an isolated recovery environment to analyze snapshots, identify clean files, remove malware, and restore data after a ransomware attack. Alternative to custom restore.
* **Isolated recovery environment (IRE)** - Secure environment (on-premises or cloud-based) where clean restore operations are performed. Can be configured for cloud-to-cloud, on-premises-to-cloud, or on-premises-to-on-premises scenarios.
* **Clean room** - Sequestered workspace within the IRE where Ransomware Resilience analyzes workloads to identify clean and impacted files. Each IRE can have up to three clean rooms.
* **Autonomous Ransomware Protection (ARP/ARP AI)** - Machine learning model within ONTAP that detects malicious file activity based on entropy patterns, file extensions, and encryption indicators. Part of the Ransomware Resilience license.
* **Protection group** - Logical grouping of workloads that can be collectively protected under a single protection strategy, simplifying management of large data estates.
* **User activity detection / Suspicious user behavior detection** - AI-driven feature that monitors for data breach and data destruction events by analyzing user activity patterns. Requires user activity agents, data collectors, and user directory connectors. This feature is powered by NetApp Data Infrastructure Insights (DII) Workload Security. In most cases, DII should not be mentioned in this context. 
  * **Data collector** - Component that collects user activity data from ONTAP systems and sends it for analysis. Created automatically when enabling protection strategies with user behavior detection.
  * **User directory connector** - Component that connects to directory services (LDAP) to map user IDs to usernames for user activity tracking and alerting.
* **Console agent** - NetApp component that ensures connectivity between on-premises storage systems and NetApp data services in the cloud.

## Typical user workflows

* **Setup and discovery** - Initial deployment involves installing Console agents, configuring licensing (90-day trial or ONTAP One license), discovering workloads across NetApp storage systems, and reviewing the protection health dashboard to identify unprotected or at-risk workloads.
* **Protection configuration** - Users review existing protection status, configure backup destinations (StorageGRID, AWS, Google Cloud, Azure), create or modify protection strategies with detection and snapshot/backup policies, optionally configure replication to secondary ONTAP sites, and set up user activity detection for enhanced threat monitoring. Protection can be applied to individual workloads or protection groups.
* **Detection and alerting** - Ransomware Resilience continuously monitors for potential attacks using ARP/ARP AI and user behavior analytics, generates alerts for potential attacks (based on encryption, file extensions, entropy) and warnings (based on new extensions, high entropy, unusual file activity), automatically creates locked snapshots when threats are detected, and sends notifications via Console notifications and email.
* **Respond to threats** - When alerts are generated, users review incident details in the Alerts dashboard, assess whether activity represents a true threat or false positive, mark alerts as "In review" during investigation, dismiss false positives (which trains the system), or mark verified threats as "Restore needed" to initiate recovery workflows.
* **Recovery** - Users can recover through standard restore (from recommended or preferred restore points at volume or file level) or clean restore (guided process through setup, analysis, planning, cleaning, and restoration phases). Clean restore offers two recovery strategies: "Latest unimpacted restore point" (fastest recovery from most recent clean snapshot) or "Least data loss" (most recent version of every unencrypted file from multiple snapshots). Recovery can be performed for all volumes, specific volumes, or individual files.
* **Reporting and governance** - Organizations monitor the protection posture through the dashboard, generate reports for alerts, protection status, readiness drills, recovery operations, and summaries, integrate with SIEM systems for security ecosystem visibility, conduct ransomware readiness drills to test preparedness, and review workload protection health metrics to maintain strong cybersecurity posture.