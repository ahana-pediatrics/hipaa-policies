# 1. Introduction

Ahana Pediatrics, Inc ("Ahana") is committed to ensuring the confidentiality, privacy, integrity, and availability of all electronic protected health information (ePHI) it receives, maintains, processes and/or transmits on behalf of its Users. As the provider of a compliant, cloud-based telemedicine platform for healthcare providers and their patients, Ahana strives to maintain compliance, proactively address information security, mitigate risk for its Users, and assure known breaches are completely and effectively communicated in a timely manner. The following documents address core policies used by Ahana to maintain compliance and assure the proper protections of infrastructure used to store, process, and transmit ePHI for Ahana Users.

Ahana provides a secure and compliant cloud-based telemedicine platform designed for healthcare providers. Our commercial relationship is with these providers, but we count their patients among our Users and our policies are designed to protect these Users as much as our healthcare professionals. Ahana is provided as a modified Software as a Service (SaaS) offering to our providers. Medical practices and professionals are not free to sign-up unilaterally, but once they are integrated into our system, things are largely self-service.

## 1.1 Software as a Service (SaaS)

<!-- TK: explain where our responsiblity starts and ends -->

As a cloud-based platform, Ahana's Users connect to the system via the Internet. Within the system, we are able to manage the security and integrity of all data flowing into and out of our networks. Data is encrypted in transit and at rest. At the perimeter of our systems, however, we are reliant on good practices by our healthcare users to ensure that any ePHI that they download, print or otherwise copy from our systems is handled in compliance with relevant guidlines. Since our healthcare provider Users are professionals in the medical field, they are expected to be well-versed and trained in HIPAA and its implications. Our patient Users are not bound by HIPAA, but are only able to access their own ePHI and so do not represent a risk.

## 1.2 Compliance Inheritance

Ahana provides a compliant cloud-based telemedicine platform for its Users. Ahana has not yet been through a third-party audit, but it uses the HITRUST CSF v9.3 to guide the creation and adherence to appropriate policies.

Ahana signs business associate agreements (BAAs) with its healthcare provider Users. These BAAs outline Ahana obligations and User obligations, as well as liability in the case of a breach. In providing a SaaS platform that adheres to the technology requirements that exist in HIPAA and HITRUST, as well as future compliance frameworks, Ahana manages various aspects of compliance for Users. The aspects of compliance that Ahana manages for Users are inherited by Users, and Ahana assumes the risk associated with those aspects of compliance. In doing so, Ahana helps Users achieve and maintain compliance, as well as mitigates Users' risk.

Ahana does not act as a covered entity. When Ahana operates only as a business associate.

Certain aspects of compliance cannot be inherited. Because of this, Ahana Users, in order to achieve full compliance or HITRUST Certification, must implement certain organizational policies. These policies and aspects of compliance fall outside of the services and obligations of Ahana.

Mappings of HIPAA Rules to Ahana controls and a mapping of what Rules are inherited by Usersß, are covered in [§2](#2-hipaa-inheritance).

## 1.3 Ahana Organizational Concepts

The physical infrastructure environment is hosted at [Amazon Web Services](https://aws.amazon.com/) (AWS). The network components and supporting network infrastructure are contained within the AWS infrastructures and managed by AWS. Ahana does not have physical access into the network components. The Ahana environment consists of AWS VPC components; CloudFront CDN servers; S3 web buckets, Node application servers; PostgreSQL database servers; Cloudwatch logging systems; Auth0 authentication services; Docker containers; and developer tool servers running on Amazon Linux.

Within the Ahana Platform on AWS all data transmission is encrypted and all storage devices are encrypted so data at rest is also encrypted; this applies to all servers. Ahana assumes all data _may_ contain ePHI, even though our Risk Assessment does not indicate this is the case, and provides appropriate protections based on that assumption.

In the case of SaaS Users, it is the responsibility of the User to restrict, secure, and assure the privacy of all ePHI data once it reaches their browser, as this is not under the control or purview of Ahana.

AWS Security Groups and NCALs are used to restrict access to only justified ports and protocols to our servers. . Ahana has implemented strict logical access controls so that only authorized personnel are given access to the internal management servers. The environment is configured so that data is transmitted from the load balancers to the application servers over a TLS encrypted session.

The bastion server, S3 web buckets, and API Gateway are externally facing and accessible via the Internet. The database servers, where the ePHI resides, are located on the internal Ahana network and can only be accessed through a bastion host. Access to the internal database is restricted to a limited number of personnel and strictly controlled to only those personnel with a business-justified reason. Remote access to internal servers is not accessible except through load balancers.

## 1.4 Requesting Audit and Compliance Reports

Ahana, at its sole discretion, shares internal audit reports, including its internal CSF assessments and Corrective Action Plans (CAPs), with customers on a case by case basis. All audit reports are shared under explicit NDA in Ahana format between Ahana and party to receive materials. Audit reports can be requested by Ahana healthcare Users.

The following process is used to request audit reports:

1. Email is sent to compliance-reports@ahanapediatrics.com. In the email, please specify the type of report being requested and any required timelines for the report.
2. Ahana staff will log an issue with the details of the request into the Ahana Support System. The Ahana Support System is used to track requests' status and outcomes.
3. Ahana will confirm if a current NDA is in place with the party requesting the audit report. If there is no NDA in place, Ahana will send one for execution.
4. Once it has been confirmed that an NDA is executed, Ahana staff will move the issue to "Under Review".
5. The Ahana Security Officer or Privacy Officer must Approve or Reject the Issue. If the Issue is rejected, Ahana will notify the requesting party that we cannot share the requested report.
6. If the issue has been Approved, Ahana will send the customer the requested audit report and complete the Quality Management System issue for the request.

## 1.5 Version Control

Refer to the GitHub repository at [https://github.com/ahana-pediatrics/hipaa-policies](https://github.com/ahana-pediatrics/hipaa-policies) for the full version history of these policies.
