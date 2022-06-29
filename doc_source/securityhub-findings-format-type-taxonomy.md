# Types taxonomy for ASFF<a name="securityhub-findings-format-type-taxonomy"></a>

The following information describes the first three levels of the `Types` path\. In the list, the top\-level bullets are namespaces, the second\-level bullets are categories, and the third\-level bullets are classifiers\. Finding providers must use defined namespaces\. The defined categories and classifiers are recommended for use, but are not required\. Only the software and configuration checks namespace has defined classifiers\. 
+ Namespaces
  + Categories
    + Classifiers

A finding provider might define a partial path for namespace/category/classifier\. For example, the following finding types are all valid\.
+ TTPs
+ TTPs/Defense Evasion
+ TTPs/Defense Evasion/CloudTrailStopped

The tactics, techniques, and procedures categories in the following list align to the [MITRE ATT&CK MatrixTM](https://attack.mitre.org/matrices/enterprise/)\. Unusual behaviors reflect general unusual behavior, such as general statistical anomalies, and are not aligned with a specific TTP\. However, you could classify a finding with both unusual behaviors and TTPs finding types\.
+ Software and Configuration Checks
  + Vulnerabilities
    + CVE
  + AWS Security Best Practices
    + Network Reachability
    + Runtime Behavior Analysis
  + Industry and Regulatory Standards
    + CIS Host Hardening Benchmarks
    + CIS AWS Foundations Benchmark
    + PCI\-DSS Controls
    + Cloud Security Alliance Controls
    + ISO 90001 Controls
    + ISO 27001 Controls
    + ISO 27017 Controls
    + ISO 27018 Controls
    + SOC 1
    + SOC 2
    + HIPAA Controls \(USA\)
    + NIST 800\-53 Controls \(USA\)
    + NIST CSF Controls \(USA\)
    + IRAP Controls \(Australia\)
    + K\-ISMS Controls \(Korea\)
    + MTCS Controls \(Singapore\)
    + FISC Controls \(Japan\)
    + My Number Act Controls \(Japan\)
    + ENS Controls \(Spain\)
    + Cyber Essentials Plus Controls \(UK\)
    + G\-Cloud Controls \(UK\)
    + C5 Controls \(Germany\)
    + IT\-Grundschutz Controls \(Germany\)
    + GDPR Controls \(Europe\)
    + TISAX Controls \(Europe\)
  + Patch Management
+ TTPs
  + Initial Access
  + Execution
  + Persistence
  + Privilege Escalation
  + Defense Evasion
  + Credential Access
  + Discovery
  + Lateral Movement
  + Collection
  + Command and Control
+ Effects
  + Data Exposure
  + Data Exfiltration 
  + Data Destruction 
  + Denial of Service 
  + Resource Consumption
+ Unusual Behaviors
  + Application
  + Network Flow
  + IP address
  + User
  + VM
  + Container
  + Serverless
  + Process
  + Database
  + Data 
+ Sensitive Data Identifications
  + PII
  + Passwords
  + Legal
  + Financial
  + Security
  + Business