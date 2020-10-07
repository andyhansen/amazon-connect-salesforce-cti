# Amazon Connect CTI Adapter v5 for Salesforce Classic

Setup and Installation Guide

<p align="center">
  <img src="./media/image1.png" />
</p>

*September, 2020*

*© Copyright Amazon.com, Inc. or its affiliates. All Rights Reserved. SPDX-License-Identifier: CC-BY-SA-4.0*

#### Notices

This document is provided for informational purposes only. It represents
AWS's current product offerings and practices as of the date of issue of
this document, which are subject to change without notice. Customers are
responsible for making their own independent assessment of the
information in this document and any use of AWS's products or services,
each of which is provided "as is" without warranty of any kind, whether
express or implied. This document does not create any warranties,
representations, contractual commitments, conditions or assurances from
AWS, its affiliates, suppliers or licensors. The responsibilities and
liabilities of AWS to its customers are controlled by AWS agreements,
and this document is not part of, nor does it modify, any agreement
between AWS and its customers.

#### Abstract

This guide provides the steps to setup the integrations between Amazon
Connect and Salesforce using the Amazon Connect CTI Adapter and Amazon
Connect Lambda Package for Salesforce.

Table of Contents
============

- Introduction
  - [Key Benefits and Requirements](01%20Introduction/01%20Key%20Benefits%20and%20Requirements.md)
- Installation
  - [Installing the Amazon Connect CTI Adapter for Salesforce Package](02%20Installation/01%20Installing%20the%20Amazon%20Connect%20CTI%20Adapter%20for%20Salesforce%20Package.md)
  - [Installing the Amazon Connect Salesforce Lambda Package](02%20Installation/02%20Installing%20the%20Amazon%20Connect%20Salesforce%20Lambda%20Package.md)
  - [Upgrading from an Earlier Version](02%20Installation/03%20Upgrading%20from%20an%20Earlier%20Version.md)
- Configuring and Using CTI Adapter Features
  - [CTI Adapter Configuration](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/01%20CTI%20Adapter%20Configuration.md)
  - [Omnipresence Agent State Sync](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/02%20Omnipresence%20Agent%20State%20Sync.md)
  - [Contact Attributes Display](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/03%20Contact%20Attributes%20Display.md)
  - [Call Recording Link for Task](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/04%20Call%20Recording%20Link%20for%20Task.md)
  - [Call Display on the Account Page](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/05%20Call%20Display%20on%20the%20Account%20Page.md)
  - [Outbound Campaign Calls](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/06%20Outbound%20Campaign%20Calls.md)
  - [Amazon Connect Reports in Salesforce](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/07%20Amazon%20Connect%20Reports%20in%20Salesforce.md)
  - [CTI Flows](03%20Configuring%20and%20Using%20CTI%20Adapter%20Features/08%20CTI%20Flows.md)
- Configuring and Using AWS Serverless Application Repository for Salesforce Features
  - [Invoking the Amazon Connect Salesforce Lambda in a Contact Flow](04%20Configuring%20and%20Using%20AWS%20Serverless%20Application%20Repository%20for%20Salesforce%20Features/01%20Invoking%20the%20Amazon%20Connect%20Salesforce%20Lambda%20in%20a%20Contact%20Flow.md)
- Appendix A: CTI Flow Sources and Events
  - [CTI Flow Sources and Events](https://github.com/amazon-connect/amazon-connect-salesforce-cti/blob/master/classic/04%20Appendix%20A:%20CTI%20Flow%20Sources%20and%20Events/01%20CTI%20Flow%20Sources%20and%20Events.md)
- Appendix B: Configuring Salesforce as Your Identity Provider
  - [Configuring Salesforce as Your Identity Provider](https://github.com/amazon-connect/amazon-connect-salesforce-cti/blob/master/classic/05%20Appendix%20B:%20Configuring%20Salesforce%20as%20Your%20Identity%20Provider/01%20Configuring%20Salesforce%20as%20Your%20Identity%20Provider.md)
- Appendix C: CTI Flow Examples
  - [CTI Flow Examples](https://github.com/amazon-connect/amazon-connect-salesforce-cti/blob/master/classic/06%20Appendix%20C:%20CTI%20Flow%20Examples/01%20CTI%20Flow%20Examples.md)
- Appendix D: CTI Flow Blocks
  - [CTI Flow Blocks](https://github.com/amazon-connect/amazon-connect-salesforce-cti/blob/master/classic/07%20Appendix%20D:%20CTI%20Flow%20Blocks/01%20CTI%20Flow%20Blocks.md)

Introduction
============

The core functionality of the Amazon Connect CTI Adapter provides a
WebRTC browser-based Contact Control Panel (CCP) within Salesforce. The
Amazon Connect CTI integration consists of two components, a [managed
Salesforce
package](https://appexchange.salesforce.com/listingDetail?listingId=a0N3A00000EJH4yUAH)
and an [AWS Serverless
application](https://aws.amazon.com/serverless/serverlessrepo/) deployed
to your AWS environment.

With those components, customers can build a deep integration between
the Amazon Connect contact center platform and Salesforce, the leading
customer relationship management (CRM) platform. The AWS Serverless
application package contains a set of common AWS Lambda functions to be
used by Amazon Connect to interact with Salesforce.

Release Notes
=============

### 5.3 September 2020
- **Bugfix**: Fix the issue that caused ACSFCCP_CallRecordingTask component to not work.

### 5.2 September 2020
- **Bugfix**: Fix the issue that prevented users from creating a new record using CTI Flows in Classic.
- **Bugfix**: Fix the issue that caused the contact channel analytics to not get updated at the end of a call.
- **Bugfix**: Fix the contact channel analytics recording view.
- **Feature**: Add a CTI block called "Get Chat Message."
- **Feature**: Add a CTI block called "SOQL Query." This block executes an arbitrary SOQL statement and returns the results.

### 5.1 Late August 2020
- **Bugfix**: Ensure "Get App View" CTI Flow block doesn\'t break the sidebar
- **Enhancement**: Add "queueARN" field to \"Dial Number\" CTI Flow block
- **Bugfix**: Ensure some required CTI Flow block fields are not shown as \"optional"
- **Bugfix**: Ensure \"Save (or Create) a Record\" block works as expected
- **Bugfix**: Fix the validation error on "CallDurationInSeconds" field in \"Create a Task\" block
- **Bugfix**: Fix phantom scrollbar on Windows machines
- **Bugfix**: Fix issue where copying contact attributes to clipboard doesn't work
- **Bugfix**: Fix issue where "saveLog" CTI Flow block throws an error
- **Bugfix**: Fix issue with onOffline CTI Flow event not firing
- **Bugfix**: Fix various omnichannel presence sync bugs
- **Bugfix**: Ensure the CCP default dimensions are adjusted to CCPv2 defaults
- **Feature:** Add block \"Set Agent Status By Name on Connect.\"

### 5.0 August 2020
- **This release has new features and updates:** Please test and validate version 5.0 in your Salesforce sandbox before upgrading this in production. 
- **CTI Flows:** CTI Flows replace Lightning CTI Extensions in allowing customers to build their agent workflows for Lightning and Classic via a drag and drop UI. Many of the CTI blocks are similar to the Lightning CTI Extension script API calls and can be mapped similarly. Lightning CTI Extension scripts are NOT automatically migrated to CTI Flows. When upgrading the package with existing scripts, it will give you the option to download the existing script for reference before building your CTI Flows. We strongly recommend you validate this install/upgrade in a test environment and fully test the CTI Flows against your previous scripts functionality. Please open a support ticket if there is additional functionality you require from your current scripting implementation. 
- **Security Profile improvements:** Added AC Administrator, AC Agent, and AC Manager permission sets to enforces objects access and fields level security (FLS) as per Salesforce security guideline for managed package. To access Amazon Connect Objects and fields, user should either one of Amazon Connect permission sets AC Administrator, AC Agent, and AC Manager. 
- **Attributes:** Amazon Connect CCP (Contact Control Panel) in Lightning and Classic now display an overlay for showing attributes consistently. 
- **AWS Secrets Manager** support for storing Salesforce credentials. 
- **VPC Support**: ability to place Lambdas in VPC 
- **New Salesforce API integration:** Exposed new operations in sfinvokeapi to read or create Salesforce records(query, queryOne, createChatterPost, createChatterComment, lookup_all, delete) 
- **Upgrade:** Amazon Connect Streams API bumped up to version 1.5. 
- **Bugfix:** Task creation issue for non-connect users - Fixed task trigger apex code, added a validation before evaluate security access check for Amazon Connect managed package objects 
- **Bugfix:** Contact interaction duration fixed. 
- **Other minor bugfixes and improvements**

### 4.5 April 2020
- **This release has new features and updates:** Please test and validate version 4.5 in your Salesforce sandbox before upgrading this in production.
- **Installation / Configuration:** AC_Administrator role has been added to manage CTI Configuration in addition to AC_Manager and AC_Agent. See documentation for further information.
- **API:** Updated support for CCPv2 in Classic/Console. See documentation for Call Center settings.
- **Bugfix:** Updated attribute display to resolve duplicated attributes.
- **Security:** Improved enforced Salesforce sharing model (record and field level) support.

### 4.4 March 2020
- **This release has significant new features and updates:** Please test and validate version 4.3 in your Salesforce sandbox before upgrading this in production.
- **Documentation:** Guide has been rewritten and restructured based on feedback.
- **Installation / Configuration:** Improved installation and configuration guide
- **Installation / Configuration:** Added Enhanced Agent Logout functionality to Lightning.
- **API:** Updated to the latest Amazon Connect Streams and Chat libraries
- **API:** Additional extensibility methods provided
- **Setup:** Improved Presence Sync Rule editor
- **Setup:** CTI Adapter validation is performed upon initialization and will inform the user of common misconfigurations.
- **Setup:** Additional CTI Script examples are provided.
- **Setup:** The ability to place the lightning transcript view on Task, Contact Channel, and Contact Channel Analytics object has been added.
- **Bugfix:** OmniChannel workload related data not being usable has been resolved.
- **Bugfix:** CTI Attribute issue when processing multiple pieces of contact attribute data has been resolved.
- **Bugfix:** The call transcript now scrolls within a fixed region rather than consuming vertical space.
- **Bugfix:** Finding Task Record in Classic/Console fixed.
- **Security:** The ability to create, update, and delete AC_CtiAdapter, AC_CtiScript, AC_CtiAttribute and AC_PresenceSyncRule records has been removed from the AC_Agent permission set.

### 4.2 December 2019
- **This release has significant new features and updates:** Please test and validate version 4.2 in your Salesforce sandbox before upgrading this in production.
- **Installation / Configuration**: Improved installation and configuration guide
- **API**: Lightning CCP Extension scripts and reference guide
- **Setup**: A default CTI adapter and scripts for click-to-dial, voice contact pop, and chat contact pop are not included in the base installation.
- **Editor**: A more robust script editor is included for use in CTI adapter / script configuration.
- **Bugfix**: SSO issue has been resolved

### 4.1 November 2019
- **This release has significant new features and updates:** Please test and validate version 4.0 in your Salesforce sandbox before upgrading this in production. As we look to simplify documentation, this release introduces a new [**Amazon Connect CTI Adapter v4 for Salesforce Lightning**](https://connect-blogs.s3.amazonaws.com/Amazon+Connect+Salesforce+CTI+Adapter/Amazon+Connect+CTI+Adapter+for+Salesforce+Lightning+-+Setup+and+Installation+Guide.pdf) setup and installation guide. Please review this setup guide in detail to see all the latest changes for Lightning CTI Adapter installations.
- **Classic and Console CTI setup guide:** Please use the [**Amazon Connect CTI Adapter v4 for Salesforce Classic**](https://connect-blogs.s3.amazonaws.com/Amazon+Connect+Salesforce+CTI+Adapter/Amazon+Connect+CTI+Adapter+for+Salesforce+Classic+-+Setup+and+Installation+Guide.pdf) setup and installation guide for Classic and Console CTI Adapter installations.
- **Amazon Connect Chat and Contact Control Panel (CCP) v2:** support for Amazon Connect chat and integration of CCP v2. CCP v2 is required for Lightning CTI Adapter installations. CCP v1 is still supported for Classic / Console CTI Adapter installations.
- **Historical and Real-Time Reporting:** updated historical metric functionality with additional metrics and dashboards. Added real-time metrics and dashboards. This functionality requires an update of AWS Serverless Lambda functions for Salesforce.
- **Lightning CCP Extensions and configuration:** We have revamped the approach for the Call Center config and have added a new AC CTI Adapters Lighting config page.
- **High Velocity Sales:** CTI Adapter integration supported for Salesforce High Velocity Sales product.

### 3.11 August 2019
- Added support for Salesforce platform encryption
- Fixed issue with logout action not re-rendering the sign-in button
- Fixed documentation issue regarding presence sync sources
- Fixed documentation issue regarding recorded conversations security configuration
- Updated documentation for presence sync rule configuration

### 3.10 July 2019
- Added support for enabling / disabling softphone popout
- Added support for previousWorkloadPct and newWorkloadPct operands in presence sync rules
- Fixed issue with presence sync rules loading

### 3.9 May 2019
- Added support for Opportunities for Task association
- Fixed issue with presence sync rules loading
- Fixed issue with state setting when no presence rules defined
- Fixed issue with Task pop in specific config scenarios

### 3.87 May 2019 
- NOTE: The "mini" Task page has been deprecated in this release of the adapter. Users requiring custom functionality may use the page and controller code included in this document as a starting point for a custom Task page of their design.
- Added rules-based configuration of agent presence state between Amazon Connect and Salesforce
- Added enhanced contact attribute display and configuration including clickable hyperlinks, key-value display options, and key-value formatting
- Added option to enable/disable automatic call duration updating on the Task object
- Added functionality to directly pop associated record on click-to-dial avoiding search and pop behavior
- Fixed issue with callback Task pops not occurring in some cases

### 3.7 May 2019 
- Unpublished version

### 3.6 April 2019
- NOTE: Automatic association of accounts, contacts, leads, or contacts to call activity (Task) records based upon tab navigation has been deprecated. Automatic association of accounts, contact, leads or contacts to call activity (Task) records when a single match is made via ANI lookup OR by contact attribute is supported.
- NOTE: The "mini" Task page will be deprecated in future releases. The default setting is now "DEFAULT_TASK_LAYOUT".
- NOTE: Automatic pop of Tasks in an object's (Account, Contact, Lead, Case) subtab is only supported with the object (Account, Contact, Lead, Case) is open in a primary tab.
- Added support for queued callback calls
- Added support for specifying call types for which to create Task objects
- Added support for enabling / disabling automatic call duration updates of call activity (Task) objects.
- Fixed issue with secondary click-to-dial in console mode
- Fixed issue with Task pop occurring during call connecting when set to start of call
- Fixed issue with call context data remaining after a call has ended
- Fixed issue with contact attributes being displayed after a call has ended or has been missed
- Fixed issue with click to dial with ani match to multiple Salesforce objects

### 3.1 March 2019
- Added ability to specify DEFAULT_TASK_LAYOUT for the Call Activity Page setting
- Added ability to specify static values used during initial task creation
- Added support for Standard Lightning navigation
- Added support for secondary click-to-dial in Console mode
- Fixed issue with primary tab closing upon call activity (Task) save
- Fixed issue with Case handling and Task association

### 3.0 February 2019
- Removed requirement for Omni-channel to be enabled to perform installation
- Added ability to specify custom ringtone
- Added ability to enable or disable the automatic creation of task (call activity) objects
- Added ability to specify a page to select creation of Lead or Contact when an object with matching ANI is not found
- Added ability specify task (call activity) object pop at the start of call, end of call, or to disable pop
- Added ability to edit task (call activity) subject
- Added automatic setting of whoId and whatId on task (call activity) objects
- Added ability to specify a custom task pop page
- Added ability to include agent friendly name when creating task (call activity) objects for calls delivered to agent queues
- Added ability to add third call participant via click to dial
- Added call attributes display in classic mode
- Fixed call attributes display being persistent when no attributes are defined
- Added ability for automatic task creation on outbound calls
- Upgraded API to amazon connect streams 1.3
- Added support for Lightning Flow Setup

Further Reading
===============

For additional information, see the following:

-   Amazon Connect CTI Adapter for Salesforce:\
    <https://appexchange.salesforce.com/appxListingDetail?listingId=a0N3A00000EJH4yUAH>

-   Amazon Connect User Guide:\
    <https://docs.aws.amazon.com/connect/latest/userguide/using-amazon-connect.html>

-   Amazon Connect Admin Guide:\
    <https://docs.aws.amazon.com/connect/latest/adminguide/what-is-amazon-connect.html>

-   Amazon Connect API Reference:\
    <https://docs.aws.amazon.com/connect/latest/APIReference/Welcome.html>

-   Amazon Connect Release Notes:\
    <https://docs.aws.amazon.com/connect/latest/adminguide/amazon-connect-release-notes.html>

-   Amazon Connect FAQ:\
    <https://aws.amazon.com/connect/faqs>