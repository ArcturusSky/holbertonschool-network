# Networking Fundamentals for Programming

- [Networking Fundamentals for Programming](#networking-fundamentals-for-programming)
  - [1. Introduction to Computer Networks](#1-introduction-to-computer-networks)
    - [1.1 What is a Computer Network?](#11-what-is-a-computer-network)
    - [1.2 Network Components](#12-network-components)
  - [2. The OSI Model](#2-the-osi-model)
    - [2.1 Overview of the 7 Layers](#21-overview-of-the-7-layers)
    - [2.2 Function of Each Layer](#22-function-of-each-layer)
  - [3. TCP/IP Model](#3-tcpip-model)
    - [3.1 Comparison with OSI Model](#31-comparison-with-osi-model)
    - [3.2 TCP/IP Layers](#32-tcpip-layers)
  - [4. IP Addressing](#4-ip-addressing)
    - [4.1 IPv4 and IPv6](#41-ipv4-and-ipv6)
    - [4.2 Public vs Private IP Addresses](#42-public-vs-private-ip-addresses)
    - [4.3 Localhost and Subnets](#43-localhost-and-subnets)
  - [5. Protocols](#5-protocols)
    - [5.1 TCP vs UDP](#51-tcp-vs-udp)
    - [5.2 Other Common Protocols](#52-other-common-protocols)
  - [6. Network Tools and Commands](#6-network-tools-and-commands)
    - [6.1 netstat](#61-netstat)
    - [6.2 ping](#62-ping)
    - [6.3 Other Useful Tools](#63-other-useful-tools)
  - [7. Network Programming Basics](#7-network-programming-basics)
    - [7.1 Sockets](#71-sockets)
    - [7.2 Basic Client-Server Model](#72-basic-client-server-model)
  - [8. Network Security Basics](#8-network-security-basics)
    - [8.1 Firewalls](#81-firewalls)
    - [8.2 Encryption (SSL/TLS)](#82-encryption-ssltls)
    - [8.3 VPNs](#83-vpns)
  - [9. Emerging Technologies](#9-emerging-technologies)
    - [9.1 Software-Defined Networking (SDN)](#91-software-defined-networking-sdn)
    - [9.2 Network Function Virtualization (NFV)](#92-network-function-virtualization-nfv)
    - [9.3 5G Networks](#93-5g-networks)
  - [10. Troubleshooting Network Issues](#10-troubleshooting-network-issues)
    - [10.1 Common Network Problems](#101-common-network-problems)
    - [10.2 Debugging Techniques](#102-debugging-techniques)
    - [10.3 Best Practices for Network Management](#103-best-practices-for-network-management)


## 1. Introduction to Computer Networks

### 1.1 What is a Computer Network?
A computer network is a set of interconnected devices that can communicate and share resources. Networks range from small home setups to global systems like the Internet.

Types of networks:
- LAN (Local Area Network): Covers a small area, typically within a building.
- WAN (Wide Area Network): Spans large geographical areas, often connecting multiple LANs.
- WLAN (Wireless LAN): A LAN that uses wireless connections.
- Other types: CAN, MAN, PAN, SAN, VPN (each serving specific purposes or scales).

### 1.2 Network Components
- Nodes: Devices like computers, servers, switches, and routers.
- Links: Physical or wireless media connecting nodes.
- Protocols: Rules governing communication (e.g., TCP/IP, HTTP).

## 2. The OSI Model

### 2.1 Overview of the 7 Layers
The OSI (Open Systems Interconnection) model is a conceptual framework describing network communication in 7 layers:

1. Physical
2. Data Link
3. Network
4. Transport
5. Session
6. Presentation
7. Application

### 2.2 Function of Each Layer
- **Physical**: Deals with physical transmission of data (e.g., cables, signals).
- **Data Link**: Ensures reliable data transfer between adjacent network nodes.
- **Network**: Handles routing and addressing for data packets.
- **Transport**: Ensures complete data transfer.
- **Session**: Manages connections between applications.
- **Presentation**: Formats and encrypts data.
- **Application**: Interfaces with end-user applications.

## 3. TCP/IP Model

### 3.1 Comparison with OSI Model
The TCP/IP model is a simplified, four-layer model used in real-world networking. It combines some OSI layers.

### 3.2 TCP/IP Layers
1. **Network Access**: Combines Physical and Data Link layers of OSI.
2. **Internet**: Equivalent to Network layer in OSI.
3. **Transport**: Same as OSI's Transport layer.
4. **Application**: Combines Session, Presentation, and Application layers of OSI.

## 4. IP Addressing

### 4.1 IPv4 and IPv6
- **IPv4**: 32-bit addresses (e.g., 192.168.1.1)
- **IPv6**: 128-bit addresses (e.g., 2001:0db8:85a3:0000:0000:8a2e:0370:7334)
- IPv6 was created to address IPv4 address exhaustion.

### 4.2 Public vs Private IP Addresses
- Public: Globally unique, used on the internet.
- Private: Used within local networks, not routable on the internet.

### 4.3 Localhost and Subnets
- Localhost (127.0.0.1): Refers to the current device.
- Subnet: A logical division of an IP network.

## 5. Protocols

### 5.1 TCP vs UDP
- TCP (Transmission Control Protocol): Connection-oriented, reliable.
- UDP (User Datagram Protocol): Connectionless, faster but less reliable.
- Common ports: SSH (22), HTTP (80), HTTPS (443)

### 5.2 Other Common Protocols
- HTTP/HTTPS: Web communication
- FTP: File transfer
- SMTP: Email transmission
- DNS: Domain name resolution

## 6. Network Tools and Commands

### 6.1 netstat
Usage: Displays network connections, routing tables, interface statistics.
Common options:
``` sh
netstat -a  # Show all connections
netstat -t  # Show TCP connections
netstat -u  # Show UDP connections
```

### 6.2 ping
Purpose: Tests connectivity between host and destination.

Basic syntax:

```sh
ping [options] destination
ping -c 4 google.com  # Send 4 pings to google.com
```

### 6.3 Other Useful Tools
- traceroute: Shows the path packets take to a destination.
- nslookup: Queries DNS servers.
- ifconfig/ipconfig: Displays network interface configuration.

## 7. Network Programming Basics

### 7.1 Sockets
Sockets are endpoints for communication between machines. They can use TCP or UDP.

### 7.2 Basic Client-Server Model
Example of a simple server in C:

```c
#include <stdio.h>
#include <sys/socket.h>
#include <arpa/inet.h>
#include <unistd.h>
#include <string.h>

int main(int argc, char const *argv[]) {
    int server_fd, new_socket;
    struct sockaddr_in address;
    int opt = 1;
    int addrlen = sizeof(address);
    char buffer[1024] = {0};
    char *hello = "Hello from server";
    
    // Creating socket file descriptor
    if ((server_fd = socket(AF_INET, SOCK_STREAM, 0)) == 0) {
        perror("socket failed");
        exit(EXIT_FAILURE);
    }
    
    // Forcefully attaching socket to the port 8080
    if (setsockopt(server_fd, SOL_SOCKET, SO_REUSEADDR | SO_REUSEPORT, &opt, sizeof(opt))) {
        perror("setsockopt");
        exit(EXIT_FAILURE);
    }
    address.sin_family = AF_INET;
    address.sin_addr.s_addr = INADDR_ANY;
    address.sin_port = htons( 8080 );
    
    // Forcefully attaching socket to the port 8080
    if (bind(server_fd, (struct sockaddr *)&address, sizeof(address))<0) {
        perror("bind failed");
        exit(EXIT_FAILURE);
    }
    if (listen(server_fd, 3) < 0) {
        perror("listen");
        exit(EXIT_FAILURE);
    }
    if ((new_socket = accept(server_fd, (struct sockaddr *)&address, (socklen_t*)&addrlen))<0) {
        perror("accept");
        exit(EXIT_FAILURE);
    }
    read( new_socket , buffer, 1024);
    printf("%s\n",buffer );
    send(new_socket , hello , strlen(hello) , 0 );
    printf("Hello message sent\n");
    return 0;
}
```

## 8. Network Security Basics

### 8.1 Firewalls
Firewalls monitor and control incoming and outgoing network traffic based on predetermined security rules.

### 8.2 Encryption (SSL/TLS)
SSL/TLS protocols secure internet communications, crucial for HTTPS.

### 8.3 VPNs
Virtual Private Networks extend private networks across public networks, ensuring secure communication.

## 9. Emerging Technologies

### 9.1 Software-Defined Networking (SDN)
SDN separates network control from forwarding functions, allowing more flexible network management.

### 9.2 Network Function Virtualization (NFV)
NFV replaces dedicated network appliances with software running on standard servers.

### 9.3 5G Networks
5G offers faster speeds, lower latency, and more device connectivity than previous generations.

## 10. Troubleshooting Network Issues

### 10.1 Common Network Problems
- Connectivity issues
- Slow network speeds
- DNS resolution problems

### 10.2 Debugging Techniques
- Using ping, traceroute, and netstat
- Checking physical connections
- Reviewing logs

### 10.3 Best Practices for Network Management
- Regular monitoring and maintenance
- Implementing security measures
- Keeping software and firmware updated
