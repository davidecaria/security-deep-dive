# Cloud Access Security Broker

## CH1: Overview 

A Cloud Access Security Broker (CASB) is an intermediate component that sits between cloud service consumers and cloud service providers. Its main role is to enforce security policies, allowing enterprises to ensure secure access to cloud-based resources. CASBs provide critical capabilities to address security gaps in an organization’s use of cloud services. It is important to note that the term CASB refers to a collection of services with various capabilities and functions. In other words, CASBs are middleware solutions that enable organizations to gain more control over the interaction between users and cloud apps.

## CH2: Key functions

CASBs provide four key capabilities:

- Visibility: CASBs offer granular visibility into cloud application usage.
- Compliance: They ensure that cloud usage complies with regulatory requirements.
- Data Security: CASBs protect sensitive data in transit and at rest.
- Threat Protection: They detect and mitigate cloud security threats.

## CH3: Key components

To achieve the basic functions of a CASB, various components are responsible for the following core pillars:

1. Discovery and Classification
2. Data Security
3. Threat Protection
4. Compliance
5. Access Control

These components can be implemented with various technologies, but their main role is to be part of an extended solution that secures cloud applications within an organization.

## CH4: Architecture of a CASB


There are three types of architectural implementations for a CASB, each with specific use cases and characteristics:

1. **API-Based CASB:**

    - Leverages the set of APIs provided by cloud applications to monitor and analyze data.
    - Applies policies and monitors cloud apps based on the data collected from the APIs.

2. **Proxy-Based CASB:**

    - Requires a proxy to redirect traffic between users and cloud apps.
    - Inspects this traffic to enforce policies and monitor apps.
    - Two subtypes:
       
        - **Forward Proxy:** Routes outbound traffic from the enterprise to the cloud through the CASB.
        - **Reverse Proxy:** Intercepts inbound traffic to the cloud service, often used for inline threat protection and data security.
   
3. **Multi-Mode CASB:**
    
    - Combines API-Based and Proxy-Based solutions to provide more flexibility and comprehensive security.

### API-Based vs Proxy-Based CASB

As the Multi-Mode CASB combines the other two architectural designs, it is crucial to understand their main differences:

| Aspect | API-Based | Proxy-Based |
| ------------------ | ------------------------------------------ | --------------------------------------------------- |
| Integration Method | Direct integration with cloud service APIs | Intercepts traffic between users and cloud services |
| Data Collection | Collects data via cloud service APIs | Inspects all traffic passing through the proxy |
| Latency | Lower latency; direct cloud service access | Higher latency; traffic routed through proxy |
| Scalability | Highly scalable; not dependent on traffic volume | Scalability can be limited by proxy capacity |
| Real-Time Monitoring | Near-real-time monitoring via API updates | Real-time monitoring by inspecting all traffic |

These are some key differences, highlighting the main aspects in which the two solutions differ.

### Proxy-Based CASB implementation

As mentioned above, there exist two types of Proxy-Based CASB: **Forward Proxy** and **Reverse Proxy** CASBs

They mainly differ in the following aspects:

1. **Deployment location:**

    - **FP:** Deployed on the client side, within the enterprise network.
    - **RP:** Deployed on the server side, in front of the cloud service.

2. **Traffic Redirection:**

    - **FP:** The redirection happens on the client side, when a user initiates a request, the traffic is redirected thought the proxy and then to the cloud service.
    - **RP:** The redirection happens on the server side, when a user sends a requests, the DNS record is pointing to the CASB that then will forward the traffic to the cloud service.

3. **Inspection:**

    - **FP:** The SSL/TLS traffic is decrypted, inspected and then re-encrypted before sending it to the user or to the cloud app.
    - **RP:** The SSL/TLS connection is cut. The traffic is inspected and then a new SSL/TLS connection is established.

4. **Authentication:**
 
    - **FP:** Enforces authentication directly a the proxy level.
    - **RP:** Integrates SSO to pass the authentication over.


### API-Based CASB implementation

Key aspects of an API-Based CASB are:

1. **Direct API Integration:** API-based CASBs connect to cloud services using the public APIs provided by the service providers. The integration typically uses OAuth tokens or API keys for authentication, ensuring secure access to the cloud service data and functions. 

2. **Discovery and Inventory:** The CASB discovers all cloud services in use by the organization by querying the APIs of known cloud providers. It builds an inventory of all cloud assets, including files, users, applications, and configurations.

3. **Data Collection and Analysis:** The CASB continuously monitors cloud service activities by making periodic API calls to collect data on user activities, file access, sharing events, and configurations. It aggregates data from multiple cloud services into a single repository for analysis.


## CH5: Use of a CASB

Having explored the technical details of a CASB architecture, it is worth mentioning the main use of a CASB. The aforementioned "Key Functions" can be achieved through the technical capabilities of the CASB. 

This means that by leveraging the technical capabilities of a CASB, functions like Visibility, Data Security, Compliance and Threat Protection can be achieved

### Visibility

A CASB achieves visibility by integrating with cloud services through APIs or proxy configurations to monitor all cloud application usage within an organization. It continuously collects and aggregates data on user activities, application interactions, and data access, providing a comprehensive view of cloud environments. By analyzing this data, the CASB can identify unauthorized or risky cloud services (shadow IT) and generate detailed reports on cloud usage patterns and potential vulnerabilities.

### Data Security 

CASBs ensure data security by implementing Data Loss Prevention (DLP) policies, encryption, and tokenization. They scan and protect sensitive data both in transit and at rest, applying encryption to safeguard data from unauthorized access or leakage. CASBs also enforce granular access controls and can block or quarantine files that violate security policies, preventing data breaches and ensuring that sensitive information is securely handled.

### Compliance  

To support compliance, CASBs enforce regulatory requirements by continuously monitoring and auditing cloud service configurations and user activities. They ensure that cloud applications adhere to industry regulations like GDPR, HIPAA, and PCI-DSS through automated policy enforcement and detailed audit logging. CASBs also generate compliance reports and alerts for potential violations, helping organizations maintain adherence to legal and regulatory standards.

### Threat protection

CASBs protect against threats by using advanced threat detection techniques, including anomaly detection and user behavior analytics (UBA). They monitor for unusual activities that may indicate compromised accounts or malicious behavior, applying real-time threat intelligence to identify and respond to potential risks. Additionally, CASBs incorporate malware scanning and sandboxing to detect and mitigate threats before they impact the organization’s cloud environments.