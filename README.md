# Host Discovery in SDN using POX

## Project Description

This project demonstrates a host discovery mechanism within a Software Defined Networking (SDN) environment using the POX controller. The system automatically identifies hosts in the network, keeps track of their connection details, and continuously updates this information based on network activity.

## Aim

- Identify hosts as they join the network  
- Store and manage host-related information  
- Display host details such as MAC, switch, and port  
- Keep the host database updated in real time  

## Prerequisites

- Ubuntu Operating System  
- Python 2.7  
- POX Controller  
- Mininet  
- Open vSwitch  

## Setup Instructions

### Install Required Packages
sudo apt update  
sudo apt install git mininet openvswitch-switch build-essential wget -y  

### Install Python 2.7
wget https://www.python.org/ftp/python/2.7.18/Python-2.7.18.tgz  
tar -xvf Python-2.7.18.tgz  
cd Python-2.7.18  
./configure  
make -j4  
sudo make install  

### Clone and Setup POX
cd ~  
git clone https://github.com/noxrepo/pox.git  
cd pox  
git checkout dart  

## File Placement
~/pox/pox/misc/host_discovery.py  

## Execution Steps

### Start the Controller
cd ~/pox  
python2 pox.py openflow.of_01 misc.host_discovery log.level --DEBUG  

### Launch the Network
sudo mn -c  
sudo mn --topo single,3 --controller=remote,ip=127.0.0.1,port=6633  

### Verify Connectivity
pingall  

## Working Principle

- A host generates network traffic  
- The switch forwards unknown packets to the controller  
- The controller processes the packet (PacketIn event)  
- Host details (MAC, switch ID, port) are extracted  
- New hosts are recorded in the database  
- Existing hosts are refreshed with updated timestamps  
- Hosts that remain inactive are removed after a timeout  

## Data Representation

hosts = {
    MAC: {
        "dpid": switch_id,
        "port": port_number,
        "last_seen": timestamp
    }
}

## Outcome

- Hosts are automatically discovered without manual input  
- Host information is maintained efficiently  
- The system reflects real-time changes in the network  
