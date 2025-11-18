# Introduction to Data Safe Haven (DSH) 

The UCL Data Safe Haven (DSH) is a secure, isolated environment where sensitive data can be stored, processed, and analyzed, 
while maintaining strict security measures to protect the confidentiality and privacy of individuals.

Data safe havens are essential for conducting research that involves sensitive information like 
healthcare data, financial records, or other personal data. They allow researchers to access and 
analyze this data while adhering to strict data protection laws and ethical guidelines. By ensuring
the security and confidentiality of sensitive data, data safe havens help build trust and foster 
collaboration in research.

# Account Services

[UCL DSH service](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven-dsh) is
composed by two parts: The **DSH Desktop** and the **DSH HPC cluster**.

The [DSH Desktop](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/dsh-data-safe-haven-portals) 
is a Windows Virtual Desktop. There are a number of virtual machines (VMs) that allows multiple concurrent interactive 
sessions. New sessions are connected to a virtual machine with the least load. For detailed information related to 
DSH Desktop, please visit the [user guide documentation and FAQ](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/data-safe-haven-user-guide-faqs).

The software available in DSH Desktop can be checked [here](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/software-and-services).

The [DSH HPC cluster](3-DSH_Cluster.md) is a set of Red Hat Enterprise Linux virtual machines in an isolated environment, and it can only be accessed from within the DSH (e.g. using DSH Desktop). Find more detailed information about [what a cluster is here.](2-Cluster_Computing.md) 

## DSH account application

DSH accounts are available to be requested by approved project Information Asset Owners (IAO) and Administrators (IAA) to users internal to UCL, as well as external collaborators. Before applying for a DSH account, users must complete the [Information Governance Assurance process](https://www.ucl.ac.uk/isd/data-safe-haven-arc-trusted-research-environment-assurance), including completion of the [**NHS Digital Data Security Awareness (NHSD) course provided by e-Learning for Health**](https://portal.e-lfh.org.uk/register) within the last 12 months. Once this course is completed, the applicant must upload the training certificate or a screenshot to the [IG Advisory Service portal](https://liveuclac.sharepoint.com/sites/ISD.IGAdvisoryService/Lists/Training%20Certification/NewForm.aspx?&pa=1), along with their name and the date the training was undertaken (note: UCL login required). This training is mandatory for all personnel with access to the DSH. For more information, please visit: <https://www.ucl.ac.uk/isd/information-governance-training-awareness-service>

Once the user has completed the training course and the Information Governance assurance process, the IAO or IAA for their project may request access with [the self-service forms](https://myservices.ucl.ac.uk/self-service) by using using the search box and the search term 'Data Safe Haven new user account'. For **internal UCL users**, please include their UCL User ID. For **external users**, please use their email address in the 'DSH User ID' field. Users must be members of at least one **share** (or project), so please include the name of the share and/or the CaseRef ID of the project when you are filling in the New User Account form.
The IAO/IAA can also add or remove additional shares, or create new shares if they don't exist, using the self-service forms. DSH users who are not a member of any share will be disabled.
More information related to the addition/removal/creation of shares and account requests can be found in the [service request page](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/service-requests#).

You will receive an email if your account is approved. All successful user account applications grant access to a DSH windows portal ([DSH Desktop](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/dsh-data-safe-haven-portals)) and access to the DSH HPC cluster from there. 

## DSH access

Once the account is created, the ISD team will provide the user with the necessary information to gain access to the DSH. 
Activating the account will require a mobile phone number or an alternative e-mail address for the user -- this is to provide the [PIN number separately 
from the Token for security purposes](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven/data-safe-haven-user-guide-faqs#Security%20&%20Tokens%20Portal). This information is stored securely and used only for this purpose. After the password and PIN has been changed, users will get access to the DSH portals and their shares.

The DSH webpage is composed of 3 [portals](https://www.ucl.ac.uk/isd/services/file-storage-sharing/data-safe-haven-dsh):
    - [DSH File Transfer Portal](https://filetransfer.idhs.ucl.ac.uk/): The ***only*** method available to transfer data in and out from DSH.
    - [DSH Applications & Data Portal](https://accessgateway.idhs.ucl.ac.uk/): Portal to access the DSH Desktop environment through the Citrix "XenApp & XenDesktop" technology.
    - [DSH Security & Tokens Portal](https://registration.idhs.ucl.ac.uk/dsc): Portal to generate tokens and change the password. 

The DSH Desktop publishes virtual desktops through the use of Citrix "XenApp & XenDesktop" technology. This is a web browser window from where users can connect to DSH Desktop from anywhere. The purpose of this functionality is to keep all information within the DSH environment secure, by utilising dedicated Citrix desktops. The data held within the environment can be manipulated by users without having the need to bring it locally to their machine.

The Data safe haven operates under a "walled garden" approach. All connections into the DSH are secured via dedicated fortigate firewall appliances. For this reason, there is no access to the internet from inside DSH, and the only way to tranfer data into or out of the DSH is through the [DSH File Transfer Portal](https://filetransfer.idhs.ucl.ac.uk/)

## Charges for use of DSH services

Data Save Haven services are free at point of use by default. 

!!! important
    Check our [Status page](6-Cluster_status_page.md) to see the current status of clusters and planned outages. 

Use of these services is subject to a common set of [terms and conditions](7-Terms_and_Conditions.md)

## Contact 

You can contact us [here](8-Contact_Us.md).
