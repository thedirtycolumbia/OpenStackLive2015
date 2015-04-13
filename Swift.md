## OpenStack Swift Object Storage
_John Dickinson (OpenStack Swift), Manzoor Brar (SwiftStack), Sergei Glushenko (Percona)_

An object is defined as a file, metadata, and GUID stored together. Objects are mutable and may be indexed.

A swift account refers to a storage area within the cluster. Accounts may have multiple containers.

Namespaces group objects together within accounts. Namespaces are similar to folders but cannot be nested.

Object names can contain "/" characters to represent hierarchy.

The number of namespaces and objects are theoretically unlimited (in practice, probably billions of files).

Object stores are a good fit for highly concurrent access across the data set without latency sensitivity.

Example use cases include web content stores, large-file workflows, document sharing, and backup storage.

Swift is split into an access layer and storage layer.

The access layer allows throughput to scale by adding proxy nodes. It also handles authentication and SSL.

The storage layer allows capacity to scale by adding nodes.

Swift uses erasure codes to reduce the storage footprint of replicated data.

Data distribution is determined by (seperate) ring data structures for accounts, containers, and objects.
