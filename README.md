# K3S LXD Installer script

Just a quick script for creating a couple of lxd containers to run a single k3s server and agent. There are a couple of things that have to be changed slightly to run under lxd, and this takes care of all of them for you.

Running it with no arguments will yield two self-explanitory containers:
- k3s-server
- k3s-agent

Here are the other options available:

                  -S: Only install k3s server container
                  -A: Only install k3s agent container
    -s <server-name>: Name to use for server container
     -a <agent-name>: Name to use for agent container
            -u <url>: (needed with -a) Url for k3s server
          -t <token>: (needed with -a) Token for k3s server
          -i <image>: lxc image name (default ubuntu:focal)

## Limitations

A couple of things you may want to be aware of:
- The overlay snapshotter doesn't seem to work well with zfs storage pools, which are a common default with lxd. This has been worked around by changing the k3s arguments to use the native snapshotter. If this isn't what you want, another option is to use the `dir` storage pool in lxd.
- If you want to access your cluster from anywhere but the host machine for these containers, you'll want to set up a bridge so that it gets an external IP address on your network.
