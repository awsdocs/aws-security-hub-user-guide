# Payment Card Industry Data Security Standard \(PCI DSS\)<a name="securityhub-standards-pcidss"></a>

The Payment Card Industry Data Security Standard \(PCI DSS\) standard in Security Hub consists of a set of AWS security best practices controls\. Each control applies to a specific AWS resource, and relates to one or more PCI DSS version 3\.2\.1 requirements\. A PCI DSS requirement can be related to multiple controls\. The details page for each PCI DSS control lists the specific PCI DSS requirements that are related to that control\. See [Viewing the list of controls for a standard](securityhub-standards-view-controls.md)\.

The PCI DSS Compliance Standard in Security Hub is designed to help you with your ongoing PCI DSS security activities\. The controls cannot verify whether your systems are compliant with the PCI DSS standard\. They can neither replace internal efforts nor guarantee that you will pass a PCI DSS assessment\. Security Hub does not check procedural controls that require manual evidence collection\.

Security Hub currently scopes the controls at the account level\. It is recommended that you enable these controls in all of your accounts that have resources that store, process, and/or transmit cardholder data\.

This standard was validated by AWS Security Assurance Services LLC \(AWS SAS\), which is a team of Qualified Security Assessors \(QSAs\) certified to provide PCI DSS guidance and assessments by the PCI DSS Security Standards Council \(PCI SSC\)\. AWS SAS have confirmed that the automated checks can assist a customer in preparing for a PCI DSS assessment\.

**Topics**
+ [AWS Config resources required for PCI DSS controls](securityhub-standards-pci-config-resources.md)
+ [PCI DSS controls](securityhub-pci-controls.md)
+ [PCI DSS controls that you might want to disable](securityhub-standards-pcidss-to-disable.md)