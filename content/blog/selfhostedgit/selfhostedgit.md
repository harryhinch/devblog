---
title: Self hosted git with Proxmox & Tailscale
description: How I set up a personal Gitea server for better code-storage habits!
date: 2025-01-19
tags: ["proxmox", "git", "gitea", "tailscale", "self-hosting"]
---

I typically don't have very useful habits when keeping my code for random projects. Every year for the holidays I always have to dig into several computers & shared drives just to try and find all my arduino code for the festive lights. Sometimes for web projects, my cloud-storage apps did not like the high volume of writes like when installing node modules, and I didn't know of an easy way to "ignore" those types of folders like you can do with git.

This year, I wanted to keep everything personal-project related all in one place. I could use github/gitlab/etc but was leaning towards self-hosted so I didn't have to rely on any 3rd party. Plus, it's fun to set things like this up for yourself! I already have a homelab running proxmox and had plenty of computational power to spare for it.

I chose Gitea since it looked pretty nice and had a turnkey proxmox template already. Setup went quite quickly, I used all the defaults when creating the container. Once it was running, connecting to the server directly in a browser brought up Gitea's web interface. After the onboarding setup I created a new repository and pushed some code to it without issue. Very nice!

To make it work seamlessly regardless of if I'm at home or about, I installed tailscale on the git server. After turning on <a href="https://tailscale.com/kb/1112/userspace-networking">userspace networking</a> since it was a VM, it was up and running no problem. The final step was to add another DNS entry for my domain name provider of my personal domain pointing to its tailscaile IP. This way, any time I try and access git.my-personal-domain.com it will respond with the local tailscale IP (something in the 100.x.y.z range) and I don't have to memorize its IP or mess with hosts files! This even works on my local home network so long as tailscale is running on the client machines. Gitea had some admin settings to use this new domain name, so now it looks a lot nicer on the web browser too, and I get to use the domain with setting upstream URLs and cloning!

If I ever want to share this git server with friends/family I can share that through tailscale too and we can use the same custom domain. Another added benefit of using my domain provider's DNS: no matter who I share it with they can access as long as they have regular internet and tailscale installed!

#### Links
 - <a href="https://tailscale.com/">Tailscale</a>
 - <a href="https://www.proxmox.com/en/products/proxmox-virtual-environment/overview">Proxmox</a>
 - <a href="https://about.gitea.com/">Gitea</a>