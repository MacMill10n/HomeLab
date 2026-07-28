# My HomeLab
This serves as a way to show what I have and planed as a set up for a Homelab, to show my interests and understanding without openly doxxing myself.

## Implemented HomeLab:

### Media Server
I have set up 2 media servers in my environment:
1. A movie Jellyfin server to host and stream all my owned movies from home to anywhere.
2. A music server using navidrome to stream my high quality music anywhere without subscriptions.

### Proxy
I have set up Nginx Proxy Manager as a way to proxy all my domain name traffic to the relevant services on my network.
I have this set up for:
- My custom Obsidian Sync for 3 vaults
- My Navidrome music server
- Sunshine and Moonlight to remote desktop into my main pc running Arch Linux
- PiHole for DNS resolution and blocking
- Local AI instances for tinkering with local AI solution

### Domains and DNS
I have set up 2 domains with CloudFlare for connecting and using my local services securely and away from home.
1. Custom domain that points to a Tailscale IP that hosts NPM to proxy into my home environment securely with HTTPS and not revealing my home IP.
2. Custom domain that is for any local services, this is to use HTTPS and certificates to connect to my home environment from within my home.

I additionally have set up PiHole and Unbound to act as a DNS resolution and blocker service to block unwanted websites and trackers on my home network.
The PiHole additionally allows me to use local DNS and assign my machines custom domain names.

### Docker and Proxmox
I currently have all my important and most used services listed above running in docker containers on a Raspberry Pi 5, due to its power efficiency.
I additionally have a second older server (Athlon II) that I use to run Proxmox that hosts any more demanding tasks, such as game servers or virtual machines for me to attack.

## Planned HomeLab:

### Websites
- I plan to set up a public facing website that will act as a portfolio for my skills and knowledge in a more appealing way than this GitHub repository.
- I additionally plan on setting up a recipe book website so that my friends, family, and I can access my recipes anywhere at anytime. This is planned to use Apache.

### Networking
- Using my current Proxmox installation, I additionally want to set up a Sophos firewall using the community edition as a learning tool for work.
- I also want to attempt to create a WiFi pineapple from scratch to learn WiFi sniffing and general WiFi auditing/security topics.

