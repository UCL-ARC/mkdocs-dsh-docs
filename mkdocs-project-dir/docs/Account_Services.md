# Introduction to Data Save Haven (DSH) 

It is a secure, isolated environment where sensitive data can be stored, processed, and analyzed, 
while maintaining strict security measures to protect the confidentiality and privacy of individuals.

Data safe havens are essential for conducting research that involves sensitive information like 
healthcare data, financial records, or other personal data. They allow researchers to access and 
analyze this data while adhering to strict data protection laws and ethical guidelines. By ensuring
the security and confidentiality of sensitive data, data safe havens help build trust and foster 
collaboration in research.

# Account Services

[UCL DSH service](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven-dsh) is
composed by two parts: The **DSH desktop** and the **DSH cluster**.

The [DSH desktop](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/dsh-data-safe-haven-portals) 
is a Windows Virtual Desktop. There are a number of virtual machines (VMs) that allows multiple concurrent interactive 
sessions. New sessions are connected to a virtual machine with the least load. For detailed information related to 
DSH Desktop, please visit the [user guide documentation and FAQ](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/data-safe-haven-user-guide-faqs).

The software available in DSH Desktop can be checked [here](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/software-and-services).

The [DSH cluster](DSH_Cluster.md) is a set of machines in an isolated environment and it is accessed only from the DSH desktop.  

## DSH account application

Internal UCL users and external users can apply for a DSH account but before to do so, the user must have completed the 
[**NHS Digital’s Data Security Awareness (NHSD) course provided by e-Learning for Health**](https://portal.e-lfh.org.uk/register)
in the last 12 months.  This training is mandatory for all members. For more information, please visit: 
https://www.ucl.ac.uk/isd/information-governance-training-awareness-service.

Once the course is finished, the applicant must upload the training certification in the [following sharepoint](https://liveuclac.sharepoint.com/sites/ISD.IGAdvisoryService/Lists/Training%20Certification/NewForm.aspx?pa=1).

**Internal UCL users**, can apply for an account to DSH clusters by filling in the following form in MyServices: https://uk.4me.io/cnQ9MjkzNw
The person must also read and sign the Acceptable Use Statement prior to submitting this request.

*Please note in order for the person to upload the training completion certificate and sign the acceptable use statement they
require an active UCL account.*

For **external users** there are some additional steps so submit this request and the instructions will be provided by the ISD team. If the user does not have a UCL account please use their email address in the 'DSH User ID' field.

Joiners must be a member of at least one **share** (or project), enter the name of the share when you are filling in the New User Account form.
You can add or remove additional shares or createn new shares if they do exist. DSH users who are not a member of any share will be disabled.
More information related to the addition/remove/creation of shares and account request can be found in the [service request page](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/service-requests#).

All granted applications give you a DSH windows portal and access to the DSH cluster from there. You will then receive an email when 
your account is approved.

## DSH account access

Once the account is created, the ISD team will provide the user with the necessary information to gain access to the DSH. 
It is required a mobile phone number or an alternative e-mail address for the user, this is to provide the [PIN number separately 
from the Token for security purposes](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/data-safe-haven-user-guide-faqs#Security%20&%20Tokens%20Portal). This information  is stored securely and used only for this purpose. After the password and PIN has been changed, users will get access to the DSH portals and their shares.

The DSH webpage is composed by 3 [portals](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/dsh-data-safe-haven-portals)
- [DSH Access (data portal)](https://accessgateway.idhs.ucl.ac.uk/vpn/index.html): Portal to access to DSH through the Citrix "XenApp & XenDesktop" technology.
- [DSH file transfer portal](https://filetransfer.idhs.ucl.ac.uk/webclient/Login.xhtml): The ***only*** method available to transfer data in and out from DSH.
- [DSH password and tokens](https://registration.idhs.ucl.ac.uk:8074/sso/): Portal to generate tokens and change the password. 

The DSH publishes virtual desktops through the use of Citrix "XenApp & XenDesktop" technology. This is a web browser window from where users can connect to DSH Desktop from anywhere. The purpose of this functionality is to keep all information within the DSH environment secure, by utilising dedicated Citrix desktops the data held within the environment can be manipulated by users without having the need to bring it locally to their machine.

The Data safe haven operates under a "walled garden" approach. All connections into the DSH are secured via dedicated fortigate firewall appliances. For this reason, there is not access to internet from inside DSH and the only way to tranfer data in/out from/DSH is through the [DSH file transfer portal](https://filetransfer.idhs.ucl.ac.uk/webclient/Login.xhtml).

## Charges for use of DSH services

Data Save Haven services are free at point of use by default.

!!! important
    Check our [Status page](Cluster_status_page.md) to see the current status of clusters and planned outages. 

Use of these services is subject to a common set of [terms and conditions](Terms_and_Conditions.md)

## Contact 

You can contact us [here](Contact_Us.md).
