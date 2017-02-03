ZeroTier Planetary Switch Users Guide
======

This manual describes the design and operation of ZeroTier and its associated services, apps, and libraries. Its intended audience includes IT professionals, network administrators, information security experts, and developers.

[ZeroTier Central](https://my.zerotier.com/), our enterprise web UI, has its own documentation that can be accessed through its interface. The high level ZeroTier rule description language used in Central also has its own documentation. This guide describes the core ZeroTier engine as deployed at endpoints as well as the deployment and operation of network controllers themselves.

## Table of Contents

1. [Introduction](#1)
2. [How it Works](#2)
   1. [VL1: The ZeroTier Peer to Peer Network](#2_1)
      1. [ZeroTier Addressing System](#2_1_1)
      2. [Encryption and Authentication](#2_1_2)
      3. [Trust Relationships](#2_1_3)
      4. [Global Roots and WAN Peer Discovery](#2_1_4)
      5. [Direct vs. Relayed Communication](#2_1_5)
      6. [LAN Peer Discovery](#2_1_6)
      7. [Federated Roots ("Moons")](#2_1_7)
      8. [Trusted Paths for Fast Local SDN](#2_1_8)
      9. [Troubleshooting Connectivity Problems](#2_1_9)
   2. [VL2: The Ethernet Virtualization Layer](#2_2)
      1. [Networks Identifiers and Controllers](#2_2_1)
      2. [Multicast](#2_2_2)
      3. [Ethernet Bridging](#2_2_3)
      4. [Certificates of Membership](#2_2_4)
      5. [Revocations and Fast Propagation](#2_2_5)
      6. [Rules Engine](#2_2_6)
      7. [Capabilities](#2_2_7)
      8. [Tags](#2_2_8)
5. [ZeroTier One: The Network Virtualization Service](#5)
   1. [Installation and Operation](#5_1)
      1. [Joining and Leaving Networks](#5_1_1)
      2. [Listing VL1 Peers for Network Troubleshooting](#5_1_2)
      3. [Joining Federated Roots ("Orbiting Moons")](#5_1_3)
   2. [Communicating With the Service](#5_2)
   3. [Operating a Network Controller](#5_3)
      1. [Controller Configuration](#5_3_1)
      2. [High Availability](#5_3_2)
      3. [Security Considerations](#5_3_3)
   4. [Mobile Apps](#5_4)
   5. [Advanced Topics](#5_5)
      1. [Static Paths and Interface Exclusion](#5_5_1)
      2. [Defining Trusted Paths](#5_5_2)
      3. [Allowing Remote Administrative Requests](#5_5_3)
      4. [Creating Federated Roots ("Moons")](#5_5_4)
      5. [Clustering and Geo-Optimized Routing](#5_5_5)
6. [Common Use Cases](#6)
   1. [SDN and General Network Virtualization](#6_1)
   2. [Replacing Conventional VPNs for Remote Access](#6_2)
      1. [Layer 2 Bridge Deployment Strategy](#6_2_1)
      2. [Layer 3 Router Deployment Strategy](#6_2_2)
      3. [Full Tunnel / Default Gateway Override](#6_2_3)
   3. [Multi-Site and Hybrid Cloud Backplane](#6_3)
      1. [Configuring for Specific Cloud Providers](#6_3_1)
         1. [Amazon](#6_3_1_1)
         2. [Microsoft Azure](#6_3_1_2)
         3. [Google Cloud](#6_3_1_3)
         4. [Digital Ocean, Vultr, Linode, OVH, etc.](#6_3_1_4)
   4. [SD-WAN for Site-to-Site Connectivity](#6_4)
      1. [Layer 2 Bridge Deployment Strategy](#6_4_1)
      2. [Layer 3 Router Deployment Strategy](#6_4_2)
   5. [Deivce (IoT) and Application Peer-to-Peer Networking](#6_5)
      1. [Running ZeroTier One in Containers and Virtual Appliances](#6_5_1)
      2. [ZeroTier One on Linux or BSD Powered IoT Devices](#6_5_2)
7. [For Developers: Connecting IoT Devices and Apps](#7)
   1. [ZeroTier SDK for Apps](#7_1)
   2. [ZeroTier Core](#7_2)
      1. [Code Layout and Design](#7_2_1)
      2. [Building and Using](#7_2_2)
7. [Licensing](#8)

------

## **1.** Introduction <a name="1"></a>
