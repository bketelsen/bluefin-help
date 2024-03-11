Bluefin comes with [Tailscale](https://tailscale.com/) integrated out of the box. The `tailscale` command is available via the command line. The [Tailscale documentation](https://tailscale.com/kb/start) will show you how to set it up. Wireguard tools are also available if you want to use another provider. 

There are two extensions for tailscale that are used in Bluefin. We started with tailscale-status but are moving to tailscale-gnome-qs in Fedora 39 and newer:

- F38: [tailscale-status](https://github.com/maxgallup/tailscale-status)
- F39: [tailscale-gnome-qs](https://github.com/joaophi/tailscale-gnome-qs)

Here's what it looks like: 

![image|258x500](upload://dJxDNGmjRPaHiakyLQxM3JI584Z.png)

Both extensions require a `sudo tailscale set --operator=$USER` so that your user account can toggle things like the VPN, etc. 

See [Managing Extensions](https://universal-blue.discourse.group/t/managing-extensions/166/1) for instructions on how to turn off the extension if you don't use Tailscale.