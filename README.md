# PASTA Threat Modeling: Sneaker Company Mobile App

[![Security](https://img.shields.io/badge/Security-Threat%20Modeling-red)](https://owasp.org/)
[![Framework](https://img.shields.io/badge/Framework-PASTA-blue)](https://en.wikipedia.org/wiki/Threat_model)
[![Status](https://img.shields.io/badge/Status-Active-green)]()

A comprehensive threat modeling analysis using the **Process for Attack Simulation and Threat Analysis (PASTA)** framework for a mobile app enabling users to buy and sell sneakers.

---

## 📋 Project Overview

This repository documents a complete 7-stage PASTA threat model for a sneaker company's new mobile application. The analysis identifies security requirements, vulnerabilities, and risk mitigation strategies before product launch.

**Business Context:**
- Marketplace platform connecting sellers and shoppers
- User authentication & account management
- Messaging between buyers and sellers
- Payment processing with multiple options
- User rating & review system
- High sensitivity to data privacy concerns

---

## 🎯 PASTA Framework Stages

### **Stage I: Business Objectives Definition**
Identify why the application exists and expected functionality.

**Key Business Objectives:**
- Seamless seller-shopper connection with secure user management
- Data privacy and responsible information handling to build user trust
- Clear, quick, and secure payment processing to maintain legal compliance

---

### **Stage II: Technological Scope**
Define the application architecture and technologies used.

**Technologies Evaluated:**
- **API (Application Programming Interface)** - Third-party service integrations
- **PKI (Public Key Infrastructure)** - AES & RSA encryption algorithms
  - AES: Encrypts sensitive data (credit cards)
  - RSA: Secure key exchange between app and devices
- **SHA-256** - Hash function for passwords and payment data
- **SQL** - Database operations for product and seller information

**Priority Technology: SQL Database**
SQL is prioritized because it directly handles sensitive user data, seller information, and financial transaction details. Database vulnerabilities create the largest attack surface for unauthorized data access and manipulation, making secure SQL implementation critical for preventing data breaches and maintaining legal compliance.

---

### **Stage III: Data Flow Analysis**
Analyze how information flows through application processes.

**Key Processes:**
- User registration & authentication
- Product search & listing retrieval
- Buyer-seller messaging
- Payment processing
- User rating submissions
- Account management

**Data Types:**
- User credentials (usernames, passwords)
- Personal information (names, addresses, contact details)
- Payment information (credit card numbers, billing addresses)
- Transaction history
- Messaging content

---

### **Stage IV: Threat Analysis**
Identify potential threats to the application and its technologies.

**Potential Threats:**
1. **Malware & Viruses** - Threat actors could deploy malware via malicious links in messages or injected code to steal payment data or user credentials
2. **SQL Injection Attacks** - Attackers could exploit unvalidated user input in search fields or login forms to access or modify the database directly, gaining unauthorized access to sensitive user and payment information
3. **Man-in-the-Middle (MITM) Attacks** - Unencrypted communications could be intercepted to steal authentication tokens or payment data
4. **Brute Force Authentication Attacks** - Automated attempts to guess user passwords and gain unauthorized account access

---

### **Stage V: Vulnerability Analysis**
Identify specific vulnerabilities that could be exploited.

**Identified Vulnerabilities:**
1. **Unvalidated SQL Queries** - If user input (search terms, usernames) isn't sanitized before being passed to SQL queries, attackers can inject malicious SQL code to bypass authentication or exfiltrate data
2. **Weak Encryption Implementation** - If AES or RSA encryption is improperly configured or uses weak key sizes, encrypted payment data and user information could be decrypted by attackers
3. **Missing Input Validation** - No validation on user inputs allows injection attacks (SQL, XSS) to be injected through message fields, search bars, or form submissions
4. **Insufficient API Authentication** - Third-party APIs lacking proper authentication mechanisms could be exploited to access or manipulate application data

---

### **Stage VI: Attack Tree Analysis**
Map attack vectors and exploitation paths.

**Attack Tree Structure:**
```
Root: Compromise User Data
├── Database Compromise
│   ├── SQL Injection
│   │   ├── Login Form
│   │   ├── Search Functionality
│   │   └── Payment Fields
│   └── Direct Database Access
│       └── Weak Credentials
├── Encryption Bypass
│   ├── Weak Encryption Keys
│   └── Implementation Flaws
├── API Exploitation
│   ├── Unvalidated Endpoints
│   └── Missing Authentication
└── Communication Interception
    ├── MITM Attack
    └── Unencrypted Transmission
```

---

### **Stage VII: Risk Mitigation Controls**
Implement defenses and safeguards to reduce security incident likelihood.

**Security Controls:**
1. **Input Validation & Sanitization** - Implement strict input validation for all user inputs and use parameterized queries (prepared statements) to prevent SQL injection attacks
2. **Multi-Factor Authentication (MFA)** - Require MFA for user accounts to prevent brute force and credential compromise attacks, especially for seller accounts with transaction access
3. **End-to-End Encryption** - Encrypt sensitive data (payments, messages, PII) using strong AES-256 encryption in transit and at rest; implement TLS 1.3 for all API communications
4. **Rate Limiting & Account Lockout** - Implement rate limiting on login attempts and auto-lockout mechanisms after failed authentication attempts to prevent brute force attacks
5. **Web Application Firewall (WAF)** - Deploy WAF to detect and block malicious traffic patterns, injection attempts, and known attack signatures before they reach the application
6. **Security Logging & Monitoring** - Implement comprehensive logging of all database queries, authentication attempts, and API calls; use SIEM tools for real-time threat detection and incident response



## 🛡️ Security Recommendations Summary

| Stage | Focus | Action Items |
|-------|-------|--------------|
| **I** | Business Goals | Define security requirements aligned with business objectives |
| **II** | Technology | Prioritize SQL database security; encrypt all sensitive data |
| **III** | Data Flow | Map all data paths; identify sensitive data handling processes |
| **IV** | Threats | Monitor for SQL injection, malware, MITM, brute force attacks |
| **V** | Vulnerabilities | Implement input validation, strong encryption, API authentication |
| **VI** | Attack Trees | Identify most critical attack paths requiring immediate mitigation |
| **VII** | Controls | Deploy MFA, WAF, rate limiting, encryption, logging & monitoring |

---

## 🔍 Key Findings

### Highest Risk Vulnerabilities
1. **SQL Injection** (High) - Most critical due to direct database access
2. **Weak Encryption** (High) - Payment data at risk of exposure
3. **Brute Force Authentication** (Medium-High) - Account takeover possible
4. **MITM Attacks** (Medium) - Interception of sensitive data in transit

### Recommended Launch Readiness
✅ **Proceed with conditions:**
- Input validation deployed on all user input fields
- AES-256 encryption implemented for data at rest
- TLS 1.3 for all API communications
- Multi-factor authentication enabled
- Rate limiting configured
- WAF deployed
- Security logging active

---

## 📚 Resources & References

- [PASTA Whitepaper]
- [OWASP Threat Modeling]
- [OWASP Top 10]
- [NIST Cybersecurity Framework]
- [CVE® Database]
- [CWE-89: SQL Injection]
- [CWE-78: OS Command Injection]
- [CWE-79: Cross-site Scripting (XSS)]

