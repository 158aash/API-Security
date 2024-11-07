# API Security in Practice - Identifying and Mitigating OWASP Vulnerabilities in crAPI 


![](/images/image.png)

  

<div align="center">

| [Overview](#overview) | [API Security in 2024](#api-security-in-2024) | [Requirements](#requirements) | [Credits](#credits) |

</div>



# Overview

  



This project focuses on identifying and mitigating vulnerabilities within the _crAPI_ (Completely Ridiculous API), aligning with the OWASP API Security Top 10 guidelines. Simulated attacks were conducted to exploit various security weaknesses commonly seen in APIs, which are prevalent and pose significant risks for enterprises. These vulnerabilities include issues like broken authentication, improper data exposure, and inadequate rate limiting, which can lead to data breaches, unauthorized access, and compromised systems.

  

After identifying each vulnerability through testing, industry-standard solutions and tools were proposed and documented to enhance API security. These include recommended authentication mechanisms, data exposure prevention techniques, rate limiting strategies, and advanced access control models. Each solution is carefully chosen to align with current industry practices, ensuring that the mitigation techniques are both relevant and effective.

**Key Objectives:**

1. **Identify Vulnerabilities:** Practical examples of the OWASP API Top 10 vulnerabilities were demonstrated using crAPI.
2. **Simulate Attacks:** Controlled tests were conducted to exploit each vulnerability, providing insights into how attackers may leverage these weaknesses.
3. **Enterprise-Grade Solutions:** A set of actionable recommendations and specific security tools were provided for each vulnerability, enabling organizations to better protect their APIs.

**Outcomes:**  
This project serves as a comprehensive guide for API security, detailing real-world API vulnerabilities and their corresponding enterprise-grade security solutions. It is designed for security teams, developers, and enterprises looking to strengthen their API defenses, align with OWASP standards, and adopt a proactive approach to secure API management.  

  

# API Security in 2024

  



  
API security is critical in 2024 due to the growing complexity and scale of API usage across organizations. The report  
**"The State of API Security in 2024"** by Imperva highlights key findings:  
  

1. **API Volume and Exposure**: With an average of **613 API endpoints discovered per account** and **1.5 billion API calls per year to enterprise sites**, the attack surface has expanded significantly, requiring robust security for each endpoint.
2. **Web Traffic Dominance**: **71% of all web traffic is API-related**, meaning that APIs are a primary conduit for data transfer and communication.
3. **Shadow and Deprecated APIs**: The presence of **29 Shadow APIs** and **16 deprecated API endpoints per account** indicates a lack of visibility and management, making it easier for attackers to exploit undocumented or outdated endpoints.
4. **Authentication Risks**: With **21 unauthenticated API endpoints** on average, attackers have ample opportunities to access sensitive data without verification.
5. **Broken Object Level Authorization (BOLA)**: Even though **1.6 BOLA API endpoints** may seem low, BOLA remains one of the most critical API vulnerabilities. Broken Object Level Authorization issues can lead to unauthorized data access, making security crucial to prevent sensitive data leaks.
6. **Targeted Attacks on Business Logic and Account Takeovers**: **27% of mitigated attacks targeted API Business Logic** and **46% of Account Takeover attacks targeted API endpoints**, illustrating how attackers are shifting towards exploiting the core functionality and identity management aspects of APIs.
7. **Financial Services Under Threat**: With **28% of DDoS attacks on APIs targeting Financial Services**, the potential impact on critical industries is substantial. Financial services are particularly vulnerable due to the high value of the data they process, making DDoS attacks and other API-related threats a pressing concern.

  

# Requirements



- crAPI
    
    **[crAPI](https://github.com/owasp/crapi)** is a platform for vehicle owners to register and manage their vehicles. Following in the footsteps of Webgoat and JuiceShop, crAPI is an intentionally vulnerable application. However, crAPI is primarily filled with API vulnerabilities for teaching, learning, and practicing API security.  
      
    crAPI specializes in the common vulnerabilities in modern API-based applications, including those in the   
    **[OWASP Top 10 for APIs](https://owasp.org/www-project-api-security/)**. We will explore various features of crAPI to discover vulnerabilities and how to mitigate them further.
    
      
    
    Requirements to install crAPI:
    
      
    
    Create a new directory named 'lab' in your home folder to organize your project files.
    
    ```Shell
    $mkdir ~/lab
    ```
    
      
    
    Navigate into the 'lab' directory you just created and download the Docker Compose configuration file for crAPI using `curl` with superuser permissions:
    
      
      
    
    ```Shell
    $ sudo curl -o docker-compose.yml <https://raw.githubusercontent.com/OWASP/crAPI/main/deploy/docker/docker-compose.yml>
    ```
    
      
    
    Create a subdirectory named 'crapi' within the 'lab' directory, move the downloaded Docker Compose file into the newly created 'crapi' directory and pull the required Docker images specified in the Docker Compose file using superuser privileges:
    
    ```Shell
    $ ls
    ```
    
    ```Shell
    $ mkdir crapi
    ```
    
    ```Shell
    $ mv docker-compose.yml crapi
    ```
    
    ```Shell
    $ cd crapi
    ```
    
    ```Shell
    $ sudo docker-compose pull
    ```
    
      
    
    Start the crAPI services in detached mode using Docker Compose:
    
    ```Shell
    $ sudo docker-compose -f docker-compose.yml --compatibility up -d
    ```
    
      
    
- Burp Suite
    
    To install Burp Suite, follow these quick steps:
    
     **Download**:
        - Navigate to the Burp Suite website and download the installer for your OS (Windows, macOS, or Linux).

    **Windows/macOS**: Run the downloaded installer and follow the on-screen instructions.

    **Linux**: Open the terminal, navigate to the downloaded file, and run:
            
     ```Shell
    $ chmod +x burpsuite_community_linux_v<version>.sh
    $ ./burpsuite_community_linux_v<version>.sh
    ```
            
     **Launch**:
        - Start Burp Suite from your Applications menu or by running the command:
            
    ```Shell
    $ burpsuite
    ```
            
     **Set Up Browser Proxy**:

    - Configure your browser to use Burp’s proxy (default: `127.0.0.1:8080`).

    - Import Burp's CA certificate to avoid SSL warnings (found in **Proxy > Options > Import/export CA certificate**).
    
      
    

  

# Credits



This project is inspired by resources and guidance from [APISEC University](https://www.apisecurity.io/)
