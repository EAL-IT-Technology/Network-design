---
layout: default
---

# High level designs

{:toc}

The purpose of high levels designs is to present to internal and external customers, what is being built.

[Layer 3 diagrams](layer3) are intented for a functional and logical overview of the system at the IP layer, whereas the HLD is about the physical devices and how they interact.

The generic HLD design documents will include
1. Introduction

    A brief introduction to the system and its functionality including information about owners and other key stakeholders.

2. Overview

    An overview of the system that in includes a diagram of the equipment and how it is connected. As opposed to Layer 3 diagrams, this includes both physical and virtual devices.

    It will also include appropriate descriptive text about what is presented

3. Security and Privacy

    A Specific measures taken to protect the system like NAT, filter rules and such.

3. Performance

    Specific perfomance criteria that the system must fullfill are listed and it is described how is it implemented.

3. Hardware

    A list of hardware included in the project. When doing the HLD, you have already established how you want to built your system and what hardware you need, so this will include a detailed list of equipment needed, as well as virtual firewall and other virtual "equipment".

4. Protocols and Standards

    A list of standards that the system uses, e.g.IEEE 802.3 ethernet.

    The list will include 2-3 sentences to give the reader an idea of what the protocol is about, and a link to an authoritative source like IEEE, rfc og IETF.

5. IP Layout and​​ VLAN​s​​ (if​ ​ applicable)

    This is a table of subnets and associated IP addresses. The table must include subnet name, ip address range, VLAN (if appl).

    If the system uses virtualization, the specific virtual network (e.g vmnet1) may be included as a column also.

    This is not the list of IP adresses of every interface on every device. That level of detail will be the lol level design.

6. Naming Convention

    This a list of how devices and other entities will be named in the system.
