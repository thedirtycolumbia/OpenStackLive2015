## Get your hands dirty with OpenStack storage: Ceph
_Csaba Balázs, Márk Korondi, Zoltán Arnold Nagy_

Ceph is software defined storage for the cloud. Ceph gives you block storage, filesystem, and object storage.

Ceph is probably amongst the top 10 most well-tested open source software projects, along with OpenStack.

Ceph allows you to provide block and object storage that is easy to scale out with no single point of failure.

As you scale out your storage you also scale out your availability guarantee becauase you increase redundancy.

New stable release come out around every 6 months, similar to the stable release schedule for OpenStack.

IBM uses the community distribution of Ceph.

OpenStack's options for ephemeral (nova), image (glance), and volume (cinder) storage can be replaced with Ceph.

If you're running RedHat 6, you should obtain qemu-rbd from Ceph's repo. RedHat 6 uses an older version of qemu.

Ceph is self-healing. Ceph trades off even data distribution for self-healing capability.

As of the time of this writing, the filesystem is not production ready, but they are seeking testers.

Ceph monitors track cluster membership and state and provide consensus.

Monitors implement a modified version of the PAXOS protocol (requires time synchronization to a local NTP server).

The maximum time difference tolerance between monitors is 50 milliseconds. This is configurable within bounds.

SoftLayer is able to georeplicate Ceph because they have dedicated bandwidth and low latency in their WAN.

An odd number of monitors are required to avoid split brain scenarios.

Object storage daemons serve objects, perform replication (you must run one per disk with a minimum of three).

By default, if any object storage daemon hits 95% disk usage it hits a hard stop.

Each object belongs to a placement group that will be replicated a configurable number of times.

With erasure codes you can lower the amount of disk needed to replicate data.

Objects are automagically distributed. Data distribution is infrastructure-aware.

CRUSH is Consistent Replication Under Scalable Hashing. See: http://www.ssrc.ucsc.edu/Papers/weil-sc06.pdf

Writes initially hit journals (best on separate SSD). You can require a write ACK to hit N replica journals.

With a SSD cache layer in front you already have a replicated persistence layer and can turn journaling off.

At the time of this writing, Ceph only has synchronous writes.

When you get to the O(10) petabyte scale the overhead of moving data around in Swift makes Ceph preferable.

Usually you run a public and private interface to Ceph where the public interface has limited functionality.
