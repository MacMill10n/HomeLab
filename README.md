# My HomeLab
This serves as a way to show what I have and planed as a set up for a Homelab, to show my interests and understanding without openly doxxing myself.

# Currently Implemented HomeLab:

I have 3 main machines that run my HomeLab:
1. A Raspberry Pi 5 for services that I want running all the time, due to it's low power requirements.
2. An old rack-mount server running an intel i7-4790K and 32gb DDR3 for running services that I do not want to eat into my daily drivers RAM. This is turned on and off as required due to the significantly higher power draw compared to the Raspberry Pi 5.
3. My daily driver PC for services that are rarely run or require a large amount of space that my "server" does not have.

## Networking
I have set up my network to allow for all my services to be accessed outside of my local network as well as easier on my local network using domain names for both.

For my local network I have the following flow and implementation in place using a dedicated domain for local services:
I have my Raspberry Pi that is connected to a network switch for all my HomeLab equipment running/doing:
-  PiHole with unbound (in a container):
   - Unbound is being for DNS filtering to block trackers using a large selection of block lists such that I can block traffic based on the devices on my network.   
   - Pihole is being used to both host unbound for the DNS filtering and blocklists as well as a local DNS resolution such that I can use a custom domain name for the machines on my network.   

- Nginx Proxy Manager (in a container):
  - This is to forward all traffic to the Raspberry Pi to the local docker container or other machine on my network hosting the service. For local services this uses a custom domain name to allow for signed certificates on my local network, as well as the custom domain name for the external network access.   

- Tailscale (on root):
  - This is so that I can connect to my local network with tailscale as a VPN.
  - This is also used for my access to services outside my network, which is detailed further on.   

For outside access to my local network, the traffic is sent/handled as follows:
- Connect to Tailscale and go to the public domain name/URL.
- The traffic is then sent to the Raspberry Pi using a local Tailscale IP address. This is done to keep ports closed on my network.
- The traffic is then accepted by Nginx Proxy Manager where it looks at the domain name given and forwards to the relevant service using signed certificates.


## Containerisation and segmentation
As to best separate my services running on my HomeLab, I use 2 major ways of segmentation:

The first is physically spreading the services across multiple machines based on the requirements I have for the services.

The second way is using containers and software defined segmentation. I use docker to create docker containers on my Raspberry Pi due to its relatively lightweight nature, this is also done on my daily driver PC as and when required. I also run Proxmox as a type 1 Hypervisor on my server to create containers to isolate my services into "types" that I can boot on and off as required.

## Services currently running

### Media Servers
My media server implementation is split into 2 categories, one that is always up and the other that I turn on and off manually.

1. The permanently up media server is my music server. This is hosted my Raspberry Pi running Navidrome as I have all my music downloaded in raw (.flac).
2. The other media server is my Jellyfin server, which is hosted on my daily driver pc. This hosts all my anime and movies that are no longer available for purchase or streaming.

### Note synchronisation
I am running Obsidian for my note taking with a community plugin that allows me to locally sync my Obsidian notes.

- The livesync plugin is installed on the machine that has Obsidian notes that require synchronisation. This connects to a couchdb that handles the storage.
- The couchdb is a service hosted on my Raspberry Pi (in a container), that is accessible locally and externally to allow for the storage of my Obsidian notes across all devices.

### Remote Control
Aside from having access to my local network through Tailscale as a VPN, I have Sunshine set up on my daily driver PC, such that I can access and control it when I am away from my local network and need to run more computationally intensive tasks.

### Website
I have a very simple nginx Apache website running on my Raspberry Pi. This website is to host all my recipes, for easy access and sharing with friends and family.

### Video game servers
The primary use for my Proxmox server currently is to host and run private video game servers.
I have 3 sets of servers currently set up:
1. My own minecraft server for myself and friends.
2. A minecraft server for my friends that I do not play on.
3. A Hytale server for myself and friends.

### Attack Boxes / Training
With my learning on TryHackMe and HackTheBox I am given machines to break into and exploit the hosts or services run on the hosts.
I have set up my own containers and environments to allow for the downloading of virtual machines with known exploits and challenges for me to attempt to gain access. The main source and use of these attack boxes is my C3SA course.

## Planned HomeLab:
I have plans and desires to set up some of the following, for personal use and learning.

### Website
- I want to set up a public facing website that will act as a portfolio for my skills and knowledge in a more appealing way than this GitHub repository.

### Networking
- Using my current Proxmox installation and a new network card, I additionally want to set up a Sophos firewall using the community edition as a learning tool for understanding corporate networking and firewalls.
- I also want to attempt to create a WiFi pineapple from scratch to learn WiFi sniffing and general WiFi auditing/security topics, using freiren/Openwrt.

