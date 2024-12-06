# linux-firewall-selinux-guide
# SELinux and Firewall Management Guide
This guide provides instructions to manage services, configure firewalls, and secure your entire Linux server using SELinux and FirewallD.

# Table of Contents
1. [SELinux Overview](#selinux-overview)
- [Protecting Services](#protecting-services)

2. [Firewall Management Using FirewallD](#firewall-mangement-using-firewalld)
- 1. [Checking Firewall State](#checking-firewall-state)
- 2. [Stopping and Starting the Firewall](#stopping-and-starting-the-firewall)
- 3. [Managing Zones in FirewallD](#manging-zones-in-firewalld)
   - a. [List Available Zones](#list-available-zones)
   - b. [List Current Zone Configuration](#list-current-zone-configuration)
   - c. [List All Zones and Their Configurations](#list-all-zones-and-their-configurations)
- 4. [ICMP Block Inversion](#imcp-block-inversion)
   - a. [Enable ICMP Block Inversion](#enable-icmp-block-inversion)
   - b. [Remove ICMP Block Inversion](#remove-imcp-block-inversion)
- 5. [Adding and Modifying Firewall Rules](#adding-and-modifying-firewall-rules)
   - a. [Block Traffic from a Specific IP](#block-traffic-from-a-specific-ip)
   - b. [Add an Interface to a Zone](#add-an-interface-to-a-zone)
   - c. [Change Interface Zone](#change-interface-zone)
   - d. [Add Specific Services or Ports](#add-specific-services-or-ports)
   - e. [Allow All UDP Traffic in a Zone](#allow-all-udp-traffics-in-a-zone)
   - f. [Add Rich Rules](#add-rich-rules)
- 6. [Reset and Reload Firewall Rules](#reset-and-reload-firewall-rules)
   - a. [Reload Rules](#reload-rules)
   - b. [Add Persistent Rules](#add-persistent-rules)
- 7. [ICMP Types](imcp-types)
   - a. [List ICMP Types](list-icmp-types)
   - b. [Block Specific ICMP Type](#block-specific-imcp-type)

3. [HTTP Service Example](#http-service-example)
   - 1. [Install and Start HTTP Service](#install-and-start-http-service)
   - 2. [Verify Default Document Root](#verify-default-document-root)
   - 3. [Add an Index File](#add-an-index-file)
   - 4. [Verify HTTP Service in Firewall](#verify-http-service-in-firewall)

4. [Additional Commands](#additional-commands)
   - a. [View All Network Interfaces](#view-all-network-interfaces)


# 1.SELinux Overview
SELinux (Security-Enhanced Linux) is a security module in Linux that enforces mandatory access control policies.

## Protecting Services

SELinux can restrict access to services and their files. Ensure SELinux policies are properly configured to secure your server.

# 2.Firewall Management Using FirewallD

FirewallD is a dynamic firewall manager that allows on-the-fly changes to rules and settings.

## 1. Checking Firewall State

![Screenshot from 2024-12-06 22-07-27](https://github.com/user-attachments/assets/dc345812-100f-40a0-a340-5e9b5f4ad80d)

Displays whether the firewall is active or inactive.

## 2. Stopping and Starting the Firewall

![Screenshot from 2024-12-06 22-09-17](https://github.com/user-attachments/assets/294d55a6-00b0-4d2f-921f-e607c755b87b)

Stops the firewall.

Use firewall-cmd --state to confirm its status.

---

![Screenshot from 2024-12-06 22-09-50](https://github.com/user-attachments/assets/fd9aa5af-ed64-4a66-8a2f-41bcf7a1b911)

start the firewall.

## 3. Managing Zones in FirewallD
### a. List Available Zones

![Screenshot from 2024-12-06 22-11-13](https://github.com/user-attachments/assets/abf8fbaa-544c-4209-bfb5-722994096174)

Shows all predefined zones like public, work, home, etc.

![Screenshot from 2024-12-06 22-14-42](https://github.com/user-attachments/assets/f8d45891-d8c4-41df-957e-edc19c47e992)

---

### b. List Current Zone Configuration

![Screenshot from 2024-12-06 22-16-29](https://github.com/user-attachments/assets/f650ffd7-aa2a-40fa-9360-e2056ccb8fef)

Displays all rules and settings for the default zone.

![Screenshot from 2024-12-06 22-50-29](https://github.com/user-attachments/assets/8561e4d1-f021-45db-af12-bfdec65fb9f4)
![Screenshot from 2024-12-06 22-53-32](https://github.com/user-attachments/assets/2878c358-fa01-4a15-8c57-4a52c818e322)



### c. List All Zones and Their Configurations

![Screenshot from 2024-12-06 22-17-53](https://github.com/user-attachments/assets/7dfa0b5e-24c0-4710-9d65-4c20cc3ea1ae)

Lists all available zones and their configurations.

## 4. ICMP Block Inversion
ICMP is used for diagnostic messages like ping.

### a. Enable ICMP Block Inversion

![Screenshot from 2024-12-06 22-32-38](https://github.com/user-attachments/assets/9a52a196-347f-4f4b-b90f-6b8197110722)

---

### b. Remove ICMP Block Inversion

![Screenshot from 2024-12-06 22-34-04](https://github.com/user-attachments/assets/c739b463-e141-4268-9d10-1b1e46cb1e9a)


## 5. Adding and Modifying Firewall Rules
### a. Block Traffic from a Specific IP

![Screenshot from 2024-12-06 22-35-00](https://github.com/user-attachments/assets/007254c7-bec0-48b7-9efc-bffbc9ee80f9)

---

### b. Add an Interface to a Zone

![Screenshot from 2024-12-06 22-37-31](https://github.com/user-attachments/assets/856b4841-de71-44cc-b077-eff27f40d9e7)


![Screenshot from 2024-12-06 22-36-41](https://github.com/user-attachments/assets/b4fb330e-b6d5-4587-89af-7f160b8cdb35)

Each interface can belong to one zone.

---

### c. Change Interface Zone

![Screenshot from 2024-12-06 22-39-06](https://github.com/user-attachments/assets/fb8ba634-587a-4a2b-aa41-ca2351ed9138)

--- 

### d. Add Specific Services or Ports

![Screenshot from 2024-12-06 22-40-23](https://github.com/user-attachments/assets/7129b7f2-1ef5-4bb6-a1ae-31cb12586a5c)

![Screenshot from 2024-12-06 22-41-11](https://github.com/user-attachments/assets/3b41a2d3-c117-4637-8cf7-42bbf70e7e56)

---

### e. Allow All UDP Traffic in a Zone

![Screenshot from 2024-12-06 22-42-00](https://github.com/user-attachments/assets/6c0c5078-3226-4c9b-954b-23d400a7ae68)

--- 

### f. Add Rich Rules

![Screenshot from 2024-12-06 22-43-41](https://github.com/user-attachments/assets/9512b375-58a5-4876-9e74-273beb3cefbb)


Allows creating complex rules like blocking SSH from a specific IP.

## 6. Reset and Reload Firewall Rules
### a. Reload Rules

![Screenshot from 2024-12-06 22-44-26](https://github.com/user-attachments/assets/013c68cd-4a74-49ac-84b3-6e632226fe4b)

Applies changes and resets temporary rules.

---

### b. Add Persistent Rules

![Screenshot from 2024-12-06 22-46-04](https://github.com/user-attachments/assets/e377f8b2-bac0-4cfc-badd-9320a30522db)

Makes rules permanent across reboots.

## 7. ICMP Types
### a. List ICMP Types

![Screenshot from 2024-12-06 22-47-00](https://github.com/user-attachments/assets/8a6d3b3a-f924-40f5-bbf8-c825d9bf4ec7)

---

### b. Block Specific ICMP Type

![Screenshot from 2024-12-06 22-47-47](https://github.com/user-attachments/assets/4d199e37-447d-44aa-a206-9848cdd64081)

# 3.HTTP Service Example
## 1. Install and Start HTTP Service

![Screenshot from 2024-12-06 23-43-26](https://github.com/user-attachments/assets/3fac1b71-53c5-465f-9244-fc381673c7fa)


## 2. Verify Default Document Root

![Screenshot from 2024-12-06 23-45-56](https://github.com/user-attachments/assets/2fa2bdc1-e13c-4866-9334-a2bee8eb4d1e)


The html folder contains the default web server files.



## 4. Add an Index File


![Screenshot from 2024-12-06 23-45-03](https://github.com/user-attachments/assets/9410a53b-d9ca-4418-87a9-2faa39834324)

## 5. Verify HTTP Service in Firewall

 ![Screenshot from 2024-12-06 23-51-32](https://github.com/user-attachments/assets/cad827ac-de51-49f7-ac7b-0ca5f23e4243)


## 4. Additional Commands
### a. View All Network Interfaces

![Screenshot from 2024-12-06 23-53-04](https://github.com/user-attachments/assets/fc4224d7-f920-4688-acaf-d4657916c009)

Now paste your ip on web browser

![Screenshot from 2024-12-06 23-52-21](https://github.com/user-attachments/assets/e50be386-c60d-4f19-9060-0296001d7203)

