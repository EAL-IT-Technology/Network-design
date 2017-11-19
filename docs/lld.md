---
layout: default
---

# Low level designs

{:toc}

## Introduction

Low level designs are about the lowest level of details, that will enable technicians and engineers to built the network and debug it.

L3 diagrams are about functionality, HLDs are about how the devices are connected and LLD goes even more into detail with specific interfaces, VLAN numbers, IP addresses, physical location and other very specific details.

When doing HLD, you can expect that the network will be very much like designed, and with LLDs you will expect more tweaking during implementation due to unforeseen details.

We will work with three parts to the low level design.
1. Spreadsheet with "numbers", like IP adresses, interfaces, connections and such
2. A floor plan which shows the physical location of devices and cables
3. A rack layout which shows where in the racks a certain device is located

Both the floor plan and rack layout might not be applicable in some designs.

## Connections

The connections document is basically a spreadsheet that combines interfaces with ip addresses and what they are connected to.

There are two groups of connections, physical and virtual.

Physical connections are from one device to another.

An example table could look like this:

| Device | Interface | Address/mask   | Subnet  | Remote device | Remote interface | Trunking | Comments                       
| :---   | :---      | :---           | :---    | :---    | :---    | :---    | :---    |
| Switch01 | ge-0/0/10  | None | N/A |  Switch02 | ge-0/0/4 | 20, 200 |  |
| Switch01 | ge-0/0/0  | 192.168.200.10 | MGNT_LAN |  Switch02 | ge-0/0/23 | N/A | Management interface |

* `Device`: The name of the physical or virtual device.

* `Interface`: The name of the interface as seen from inside the device, e.g. `ge-0/0/0`, `ens3`, `eth1` or `em2`

* `Address/mask`: The addres on the interface.

    If the address is set using DHCP, write "DHCP" in the `Address/mask` column.

    If a device has multiple IP addresses, make multiple entries in the table.

* `subnet`: the subnet that is connected to. This will be a subnet that exists in the ip scheme section of the HLD.
* `remote device`: The name of the physical or virtual device that is connected to.
* `remote interface`: the physicla port the cable is connected to at the other end.
* `trunking`: the VLANs running in the specific cable
* `comment`: a free text area for comments that may help the engineer understand some detail about the interface.

Virtual connections include VLANs and associated virtual interfaces. Virtual interfaces has the special property, that they are connected to a subnet, and not a remote device.

An example table could look like this:

| Device | Interface | Address/mask   | Subnet  | Comment |
| :---   | :---      | :---           | :---    | :--- |
| vSRX01 | ge-0/0/0.20  | 192.168.20.1/24 | USR_LAN | Serves DHCP to the subnet|
| vSRX01 | ge-0/0/0.100  | 192.168.100.1/24 | SRV_LAN | |
| vSRX01 | ge-0/0/0.200  | 192.168.200.1/24 | MGNT_LAN | |


* `Device`: The name of the virtual device.
* `Interface`: The name of the interface as seen from inside the device, e.g. `ge-0/0/0`, `ens3`, `eth1`, `em2` or `ge-0/0/0.300`
* `Address/mask`: As per physical
* `Subnet`: As per physical
* `Comment`: As per physical


Sometimes more columns are needed like `OSPF area`, `family`, `cable id` or other information that most connections must include in the specific system.



## Floor plan

The purpose of a floorplan is to physically map where a given device is located. When multiple devices are spread out in a building or buildings, locating a specific device can be tricky, so a floor plan is made to help engineers set up and troubleshoot.

It will also include how cables are drawn. This will have the added benefit of giving an idea of the length of cable, and whether or not that could affect perfomance.

This is even more relevant for wireless devices, where specialized "heatmaps" of reception is usually made.

To create a floorplan, a detailed drawing of rooms is used. All devices will be added and the connecting physical cables are drawn. Remember to add the connection point(s) where the internet connection enters the building.

A good test is to compare the floor plan to the HLD to ensure consistency


## Rack layout

The purpose of the rack layout is the show where the devices are put in the rack and to ensure that there is room enough in the racks.

When talking about racks, usually there will be refered to 19" racks. All rack devices will have a value for how many "units" of space it requires - this is a standard value of approximately 4,45 cm. A simple rack server may be 1U and other equipment 2-3-4-5U. The rack cabinet will also have a depth, so that has to be taken into consideration also.

The rack cabinet come in many heights - some as flight cases for transportation, some for server rooms and some for a patch panel/switch combination.

A long with the rack layout, a description of the cable color coding may be included. Suggested is that "red" cables are used for sensitive or public network traffic.
