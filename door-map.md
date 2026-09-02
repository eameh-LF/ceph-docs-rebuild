---
title: Ceph docs rebuild, door map
permalink: /door-map/
---

# Ceph docs rebuild: door map

Companion to the Ceph Docs Rebuild proposal. Drafted 2 September 2026 against ceph/ceph main at commit d78578929f9 (616 .rst pages). Every table below is a proposal for the team to correct; the Ambiguities section lists the judgment calls that need a decision.

## Map of old pages to new homes

Draft against upstream `main` at commit d78578929f9 (3 September 2026), read from the `doc/` tree. Titles are each file's first document heading (overline or underline form). Doors follow the proposal: 1 Start here, 2 Deploy, 3 Operate, 4 Storage services (Block, File, Object, Kubernetes), 5 Troubleshoot, 6 Reference, 7 Develop and contribute. Parts inside a service: Learn, Set up, Operate, Troubleshoot, Reference. For Deploy and Operate pages the same five words are used where they fit.

Inventory on main: 616 `.rst` files (the proposal's "568 pages" excludes the 51 man pages and a few includes). Top-level root toctree has 26 entries, not 23: `csi/index`, `technical-charter` and `crimson/crimson` are missing from the proposal's list. Per-directory counts on main today: rbd 41 (proposal 41), radosgw 76 (75), cephfs 57 (53), rados 72 (66), cephadm 27 + install 15 = 42 (40), dev 154 (143).

Marks used in the note column: `hub` = toctree-only page that dissolves into navigation; `stub` = under about 25 lines with no real content; `external` = integration with software outside Ceph; `mixed` = clearly mixes concept and procedure (or procedure and reference) and must be split under the three-type template; `long (N)` = line count that forces a split under one-task-per-procedure; `deprec` = carries a deprecation or obsolescence notice.

## Top-level mapping

Every entry in `doc/index.rst` (in toctree order), then every top-level directory and root file not in the toctree.

| Root entry or directory | Pages | Door | Reason |
|---|---|---|---|
| start/index | 7 | 1 Start here (3), 2 Deploy (2), 7 Develop (2) | Intro and beginner's guide open the journey; hardware and OS recommendations are Deploy requirements; get-involved and documenting-ceph are contributor pages |
| install/index | 15 | 2 Deploy (11), 4 Block (1), 5 (1), 7 (2) | Deployment method chooser plus package and manual install; QEMU install belongs to Block; build and clone are developer tasks |
| cephadm/index | 27 | 2 Deploy (6), 3 Operate (15), 4 Services (5), 5 (1) | Bootstrap, adoption and upgrade are Deploy; host and service management are day two; MDS, RGW, NFS, SMB and iSCSI service pages are each service's Set up |
| rados/index | 72 | 3 Operate (35), 5 Troubleshoot (9), 6 Reference (28) | Directory already splits into operations, troubleshooting, configuration and api; the split maps almost one to one onto doors |
| cephfs/index | 57 | 4 File | Whole directory is the File service |
| rbd/index | 41 | 4 Block | Whole directory is the Block service (includes iSCSI and NVMe-oF gateways) |
| radosgw/index | 76 | 4 Object | Whole directory is the Object service (includes S3 and Swift API reference) |
| csi/index | 6 | 4 Kubernetes | Already shaped as Learn plus Set up per backend |
| mgr/index | 29 | 3 Operate (19), 4 Services (4), 2 (1), 6 (2), 7 (3) | Module guides are operator pages; nfs, smb, rgw and mds_autoscaler belong to services; rook is a deployment backend; RESTful and CLI API to Reference; module authoring to Develop |
| mgr/dashboard | (in mgr) | 3 Operate | Dashboard is a day-two management surface; its 1752 lines split into set up, operate and reference within Operate |
| monitoring/index | 1 | 3 Operate | Monitoring overview and metric catalogue |
| api/index | 2 | 6 Reference | API hub and generated mon command API |
| architecture/index | 9 | 1 Start here | "Architecture in brief" lives in Door 1; two deep pages (ceph-protocol, extending-ceph) could move to Door 7 |
| Developer Guide (dev/developer_guide/index) | 19 | 7 Develop | Contributor track |
| dev/internals | 135 | 7 Develop | Internals track; about 20 pages are user-facing and are listed in the dev family map |
| governance | 1 | 7 Develop | Project governance |
| Technical Charter (technical-charter) | 1 | 7 Develop | Project governance |
| foundation | 1 | 7 Develop | Project governance |
| ceph-volume/index | 24 | 6 Reference | Subcommand reference pages; one provisioning procedure should be written in Operate and link here |
| crimson/crimson | 1 | 2 Deploy | Tech preview page whose bulk is "Deploying Crimson with Cephadm"; flags and metrics sections are Reference |
| releases/general | 1 | 6 Reference | Release cadence and lifecycle; link from Door 1 ("which release") and Door 2 (upgrades) |
| releases/index | 21 | 6 Reference | Release timeline plus 20 per-release notes |
| security/index | 14 | 7 Develop (4), 6 Reference (10) | Vulnerability reporting process is project process; the CVE list is a reference |
| hardware-monitoring/index | 1 | 3 Operate | Node-proxy hardware monitoring; deploy procedure plus limitations; its "For Developers" section is Door 7 |
| Glossary (glossary) | 1 | 6 Reference | Glossary |
| Tracing (jaegertracing/index) | 1 | 3 Operate | Enabling Jaeger tracing on a running cluster; Door 5 links to it |
| man/ (not in root toctree; built through man_index.rst and per-service man hubs) | 51 | 6 Reference | Man pages are the CLI reference; 6 of the 51 are missing from man_index.rst (ceph-bluestore-tool, ceph-kvstore-tool, ceph-monstore-tool, ceph-objectstore-tool, mount.fuse.ceph, rgw-gap-list) |
| man_index.rst | 1 | 6 Reference | Build-only toctree for the man builder |
| index.rst | 1 | 1 Start here | Root landing; rewritten as the seven-door front page |
| changelog/ | 69 .txt | 6 Reference | Historical per-version changelogs (not rst); archive or link from release notes |
| mon/ | 0 rst | 7 Develop | One dot diagram and README for paxos; developer material |
| images/, _static/, _templates/, _themes/, _ext/, scripts/ | 0 rst | none | Build assets and Sphinx extensions; no door |

Door totals from this mapping (all 616 files): Door 1 = 13, Door 2 = 21, Door 3 = 72, Door 4 = 190 (Block 43, File 63, Object 78, Kubernetes 6), Door 5 = 11, Door 6 = 141, Door 7 = 168.

## Page-by-page maps

### start/ (7 pages)

| path | title | door | part | note |
|---|---|---|---|---|
| start/index.rst | Intro to Ceph | 1 Start here | Learn | landing: component overview plus two toctrees; rewrite as the Door 1 landing |
| start/beginners-guide.rst | Beginner's Guide | 1 Start here | Learn | mixed: component concepts followed by cephadm bootstrap steps; split into a concept and a quick start |
| start/quick-rbd.rst | Block Device Quick Start | 1 Start here | Set up | not in start/index toctree; reachable only via rbd/iscsi-target-cli.rst; pre-cephadm content; rewrite as a quick start or retire |
| start/hardware-recommendations.rst | Hardware Recommendations | 2 Deploy | Learn | requirements; long (672); sizing tables are Reference material |
| start/os-recommendations.rst | OS Recommendations | 2 Deploy | Reference | platform support matrix by release |
| start/get-involved.rst | Get Involved in the Ceph Community! | 7 Develop | n/a | community channel table; also link from Door 1 footer and the Door 5 "get help" page |
| start/documenting-ceph.rst | Documenting Ceph | 7 Develop | n/a | long (1095); overlaps dev/documenting.rst and dev/generatedocs.rst; merge the three |

### install/ (15 pages)

| path | title | door | part | note |
|---|---|---|---|---|
| install/index.rst | Installing Ceph | 2 Deploy | Learn | deployment-method chooser (cephadm, Rook, others, manual, Windows); reuse as Door 2 landing |
| install/index_manual.rst | Installation (Manual) | 2 Deploy | Set up | hub |
| install/get-packages.rst | Get Packages | 2 Deploy | Set up | mixed procedure and reference (repo URLs, signing keys); 417 lines |
| install/get-tarballs.rst | Downloading a Ceph Release Tarball | 2 Deploy | Set up | stub (13 lines); merge into get-packages |
| install/mirrors.rst | Ceph Mirrors | 2 Deploy | Reference | mirror list plus "how to run a mirror" |
| install/containers.rst | Ceph Container Images | 2 Deploy | Reference | image names and tag conventions; concept plus reference |
| install/install-storage-cluster.rst | Install Ceph Storage Cluster | 2 Deploy | Set up | manual package install (APT, RPM) |
| install/manual-deployment.rst | Manual Deployment | 2 Deploy | Set up | long (585); one procedure per daemon after the split |
| install/manual-freebsd-deployment.rst | Manual Deployment on FreeBSD | 2 Deploy | Set up | platform-specific; deprec; mark legacy |
| install/install-vm-cloud.rst | Install Virtualization for Block Device | 4 Block | Set up | external (QEMU, libvirt packages); sits with rbd/qemu-rbd and rbd/libvirt |
| install/clone-source.rst | Cloning the Ceph Source Code Repository | 7 Develop | n/a | developer task |
| install/build-ceph.rst | Build Ceph | 7 Develop | n/a | developer task; overlaps dev/developer_guide/essentials |
| install/windows-install.rst | Installing Ceph on Windows | 2 Deploy | Set up | orphan (reached by :ref: only); Windows client install |
| install/windows-basic-config.rst | Windows basic configuration | 2 Deploy | Set up | orphan; short |
| install/windows-troubleshooting.rst | Troubleshooting Ceph on Windows | 5 Troubleshoot | Troubleshoot | orphan |

### cephadm/ including cephadm/services/ (27 pages)

| path | title | door | part | note |
|---|---|---|---|---|
| cephadm/index.rst | Cephadm | 2 Deploy | Learn | landing plus toctree; links dev/cephadm/index as "Cephadm Feature Planning" (developer design docs in user nav) |
| cephadm/compatibility.rst | Compatibility and Stability | 2 Deploy | Reference | container engine and OS support matrix |
| cephadm/install.rst | Using Cephadm to Deploy a New Ceph Cluster | 2 Deploy | Set up | long (612); mixed: requirements, bootstrap options, adding hosts, adding OSDs, deploying services; split into several procedures |
| cephadm/adoption.rst | Converting an Existing Cluster to Cephadm | 2 Deploy | Set up | procedure |
| cephadm/upgrade.rst | Upgrading Ceph | 2 Deploy | Operate | proposal places upgrades in Deploy; procedure plus a troubleshooting section |
| cephadm/client-setup.rst | Basic Ceph Client Setup | 2 Deploy | Set up | short procedure |
| cephadm/docker-live-restore.rst | Cephadm and Docker Engine: Live Restore | 3 Operate | Operate | niche |
| cephadm/host-management.rst | Host Management | 3 Operate | Operate | long (782); mixed procedure and reference (labels, maintenance mode, host spec) |
| cephadm/services/index.rst | Service Management | 3 Operate | Operate | long (965); mixed: service spec concept, procedures, spec schema reference; schema goes to Door 6 |
| cephadm/services/mon.rst | MON Service | 3 Operate | Operate | |
| cephadm/services/mgr.rst | MGR Service | 3 Operate | Operate | short |
| cephadm/services/osd.rst | OSD Service | 3 Operate | Operate | long (1320); mixed: drive group concept, procedures, spec reference; split |
| cephadm/services/monitoring.rst | Monitoring Services | 3 Operate | Set up | long (692); Prometheus, Grafana, Alertmanager, node-exporter; mixed |
| cephadm/services/snmp-gateway.rst | SNMP Gateway Service | 3 Operate | Set up | |
| cephadm/services/mgmt-gateway.rst | Management Gateway | 3 Operate | Set up | |
| cephadm/services/oauth2-proxy.rst | OAuth2 Proxy | 3 Operate | Set up | SSO; security |
| cephadm/services/tracing.rst | Tracing Services | 3 Operate | Set up | short; duplicates the deployment steps in jaegertracing/index |
| cephadm/services/custom-container.rst | Custom Container Service | 3 Operate | Set up | |
| cephadm/certmgr.rst | Certificate Management | 3 Operate | Operate | security |
| cephadm/operations.rst | Cephadm Operations | 3 Operate | Operate | long (1032); grab-bag: logs, daemon control, cluster shutdown and startup, CEPHADM_* health checks, config; mixes Operate, Troubleshoot and Reference; split |
| cephadm/version-tracker.rst | Version Tracking for Ceph | 3 Operate | Operate | new feature page; procedure plus reference |
| cephadm/services/mds.rst | MDS Service | 4 File | Set up | deploy MDS with cephadm; overlaps cephfs/add-remove-mds |
| cephadm/services/rgw.rst | RGW Service | 4 Object | Set up | long (597); mixed spec reference and procedures; deprec |
| cephadm/services/nfs.rst | NFS Service | 4 File (NFS) | Set up | 512 lines; overlaps mgr/nfs.rst |
| cephadm/services/smb.rst | SMB Service | 4 File (SMB) | Set up | overlaps mgr/smb.rst |
| cephadm/services/iscsi.rst | iSCSI Service | 4 Block | Set up | legacy gateway |
| cephadm/troubleshooting.rst | Troubleshooting | 5 Troubleshoot | Troubleshoot | 597 lines; linked from the Door 5 hub |

### rbd/ (41 pages, all Door 4 Block)

Also mapped into Block from elsewhere: install/install-vm-cloud.rst (Set up) and cephadm/services/iscsi.rst (Set up). No page in rbd/ is a troubleshooting page: the Block Troubleshoot part is a gap.

| path | title | door | part | note |
|---|---|---|---|---|
| rbd/index.rst | Ceph Block Device | 4 Block | Learn | landing: concept intro plus five toctree hubs (Basic Commands, Operations, Integrations, Manpages, APIs) |
| rbd/rados-rbd-cmds.rst | Basic Block Device Commands | 4 Block | Set up | mixed procedure and reference (create pool, create image, resize, remove, trash); split into Set up procedures and point at man/8/rbd |
| rbd/rbd-operations.rst | Ceph Block Device Operations | 4 Block | Operate | hub |
| rbd/rbd-snapshot.rst | Snapshots | 4 Block | Operate | mixed: layering and copy-on-write concept plus procedures; 368 lines |
| rbd/rbd-exclusive-locks.rst | RBD Exclusive Locks | 4 Block | Learn | concept with a blocklisting note |
| rbd/rbd-mirroring.rst | RBD Mirroring | 4 Block | Operate | long (633); mixed: concept, Set up (pool and peer config), Operate (promote, demote, status); split |
| rbd/rbd-live-migration.rst | Image Live-Migration | 4 Block | Operate | 416 lines; concept intro then procedures |
| rbd/rbd-persistent-read-only-cache.rst | RBD Persistent Read-only Cache | 4 Block | Set up | mixed concept and configuration |
| rbd/rbd-persistent-write-log-cache.rst | RBD Persistent Write Log Cache | 4 Block | Set up | mixed concept and configuration |
| rbd/rbd-encryption.rst | Image Encryption | 4 Block | Operate | mixed: format concept plus procedures |
| rbd/rbd-config-ref.rst | Config Settings | 4 Block | Reference | confval generated; Block Reference entry built from source |
| rbd/rbd-replay.rst | RBD Replay | 4 Block | Operate | short (42); fold into the rbd-replay man pages |
| rbd/rbd-integrations.rst | Ceph Block Device 3rd Party Integration | 4 Block | Set up | hub |
| rbd/rbd-ko.rst | Kernel Module Operations | 4 Block | Set up | client mapping; short |
| rbd/qemu-rbd.rst | QEMU and Block Devices | 4 Block | Set up | external |
| rbd/libvirt.rst | Using libvirt with Ceph RBD | 4 Block | Set up | external; 320 lines |
| rbd/rbd-kubernetes.rst | Block Devices and Kubernetes | 4 Block | Set up | stub (32) pointing at csi/rbd; merge into 4 Kubernetes |
| rbd/rbd-nomad.rst | Block Devices and Nomad | 4 Block | Set up | external (Ceph-CSI on Nomad); 476 lines; belongs with 4 Kubernetes (CSI) |
| rbd/rbd-openstack.rst | Block Devices and OpenStack | 4 Block | Set up | external |
| rbd/rbd-cloudstack.rst | Block Devices and CloudStack | 4 Block | Set up | external |
| rbd/rbd-windows.rst | RBD on Windows | 4 Block | Set up | Windows client; mixed Set up, Operate and Troubleshoot |
| rbd/iscsi-overview.rst | Ceph iSCSI Gateway | 4 Block | Learn | hub plus concept; ceph-iscsi is legacy, NVMe-oF is the successor |
| rbd/iscsi-requirements.rst | iSCSI Gateway Requirements | 4 Block | Set up | |
| rbd/iscsi-targets.rst | iSCSI Targets | 4 Block | Set up | hub |
| rbd/iscsi-target-cli.rst | Configuring the iSCSI Target using the Command Line Interface | 4 Block | Set up | 266 lines; carries the only toctree link to start/quick-rbd |
| rbd/iscsi-target-cli-manual-install.rst | Manual ceph-iscsi Installation | 4 Block | Set up | |
| rbd/iscsi-target-ansible.rst | Configuring the iSCSI Target using Ansible | 4 Block | Set up | external (ceph-ansible); deprec; retire |
| rbd/iscsi-initiators.rst | Configuring the iSCSI Initiators | 4 Block | Set up | hub |
| rbd/iscsi-initiator-linux.rst | iSCSI Initiator for Linux | 4 Block | Set up | client-side procedure |
| rbd/iscsi-initiator-win.rst | iSCSI Initiator for Microsoft Windows | 4 Block | Set up | client-side procedure |
| rbd/iscsi-initiator-esx.rst | iSCSI Initiator for VMware ESX | 4 Block | Set up | client-side procedure |
| rbd/iscsi-monitoring.rst | Monitoring Ceph iSCSI gateways | 4 Block | Operate | |
| rbd/nvmeof-overview.rst | Ceph NVMe-oF Gateway | 4 Block | Learn | hub plus concept (HA gateway groups) |
| rbd/nvmeof-requirements.rst | NVMe-oF Gateway Requirements | 4 Block | Set up | short |
| rbd/nvmeof-target-configure.rst | Installing and Configuring NVMe-oF Targets | 4 Block | Set up | |
| rbd/nvmeof-initiators.rst | Configuring the NVMe-oF Initiators | 4 Block | Set up | hub |
| rbd/nvmeof-initiator-linux.rst | NVMe/TCP Initiator for Linux | 4 Block | Set up | |
| rbd/nvmeof-initiator-esx.rst | NVMe/TCP Initiator for VMware ESX | 4 Block | Set up | |
| rbd/man/index.rst | Ceph Block Device Manpages | 4 Block | Reference | hub over man/8; dissolve into Door 6 |
| rbd/api/index.rst | Ceph Block Device APIs | 4 Block | Reference | stub hub (8 lines) |
| rbd/api/librbdpy.rst | Librbd (Python) | 4 Block | Reference | automodule API page; built into Door 6 |

### cephfs/ (57 pages, all Door 4 File)

Also mapped into File from elsewhere: cephadm/services/mds.rst, cephadm/services/nfs.rst, cephadm/services/smb.rst, mgr/nfs.rst, mgr/smb.rst, mgr/mds_autoscaler.rst (63 pages in total).

| path | title | door | part | note |
|---|---|---|---|---|
| cephfs/index.rst | Ceph File System | 4 File | Learn | landing; toctrees already grouped as Administration, Mounting, Concepts, Troubleshooting and Disaster Recovery, Developer Guides (group headings hidden inside raw HTML comments) |
| cephfs/createfs.rst | Create a Ceph file system | 4 File | Set up | mixed: pool and layout concepts plus procedure |
| cephfs/administration.rst | CephFS Administrative commands | 4 File | Reference | fs command reference with confval |
| cephfs/multifs.rst | Multiple Ceph File Systems | 4 File | Learn | concept; short |
| cephfs/add-remove-mds.rst | Deploying Metadata Servers | 4 File | Set up | mixed: hardware sizing, cephadm and manual deploy; overlaps cephadm/services/mds |
| cephfs/standby.rst | Terminology | 4 File | Operate | file has no document title (first heading is Terminology; index labels it MDS failover and standby configuration); mixed concept and config |
| cephfs/cache-configuration.rst | MDS Cache Configuration | 4 File | Reference | confval plus guidance; mixed |
| cephfs/mds-config-ref.rst | MDS Config Reference | 4 File | Reference | confval generated |
| cephfs/nfs.rst | NFS | 4 File (NFS) | Set up | short pointer page to mgr/nfs |
| cephfs/app-best-practices.rst | Application best practices for distributed file systems | 4 File | Learn | |
| cephfs/fs-volumes.rst | FS Volumes and Subvolumes | 4 File | Operate | long (1858); mixed concept and command reference; split into concept, procedures and CLI reference; deprec |
| cephfs/quota.rst | CephFS Quotas | 4 File | Operate | mixed concept and procedure |
| cephfs/health-messages.rst | CephFS health messages | 4 File | Troubleshoot | reference list of MDS health codes; feeds the Door 5 hub |
| cephfs/upgrading.rst | Upgrading the MDS Cluster | 4 File | Operate | short procedure; link from Door 2 upgrade |
| cephfs/cephfs-top.rst | CephFS Top Utility | 4 File | Operate | tool page; duplicates man/8/cephfs-top |
| cephfs/cephfs-tool.rst | cephfs-tool | 4 File | Reference | CLI reference; no man page |
| cephfs/snap-schedule.rst | Snapshot Scheduling Module | 4 File | Operate | mgr module doc that lives in cephfs; correct home |
| cephfs/cephfs-mirroring.rst | CephFS Snapshot Mirroring | 4 File | Operate | long (1466); mixed concept, Set up and Operate; duplicates dev/cephfs-mirroring.rst; deprec |
| cephfs/cephfs-mirroring-checkpoints.rst | CephFS Snapshot Mirroring Checkpoints | 4 File | Operate | |
| cephfs/purge-queue.rst | Purge Queue | 4 File | Learn | concept plus confval |
| cephfs/client-config-ref.rst | Client Configuration | 4 File | Reference | confval generated |
| cephfs/client-auth.rst | CephFS Client Capabilities | 4 File | Set up | 541 lines; mixed concept and procedure |
| cephfs/mount-prerequisites.rst | Mount CephFS: Prerequisites | 4 File | Set up | |
| cephfs/mount-using-kernel-driver.rst | Mount CephFS using Kernel Driver | 4 File | Set up | deprec note |
| cephfs/mount-using-fuse.rst | Mount CephFS using FUSE | 4 File | Set up | |
| cephfs/ceph-dokan.rst | Mount CephFS on Windows | 4 File | Set up | Windows client |
| cephfs/kernel-features.rst | Supported Features of the Kernel Driver | 4 File | Reference | |
| cephfs/mds-states.rst | MDS States | 4 File | Learn | concept; doubles as a state table |
| cephfs/posix.rst | Differences from POSIX | 4 File | Learn | |
| cephfs/mds-journaling.rst | MDS Journaling | 4 File | Learn | concept plus confval |
| cephfs/file-layouts.rst | File layouts | 4 File | Operate | mixed concept and procedure (xattrs) |
| cephfs/mdcache.rst | CephFS Distributed Metadata Cache | 4 File | Learn | |
| cephfs/dynamic-metadata-management.rst | CephFS Dynamic Metadata Management | 4 File | Learn | |
| cephfs/cephfs-io-path.rst | Ceph File System I/O Path | 4 File | Learn | |
| cephfs/charmap.rst | CephFS Directory Entry Name Normalization and Case Folding | 4 File | Operate | mixed concept and procedure |
| cephfs/lazyio.rst | LazyIO | 4 File | Learn | concept plus usage |
| cephfs/dirfrags.rst | Configuring Directory fragmentation | 4 File | Learn | concept plus config |
| cephfs/multimds.rst | Configuring multiple active MDS daemons | 4 File | Operate | mixed concept and procedure (pinning) |
| cephfs/snapshots.rst | CephFS Snapshots | 4 File | Operate | short; overlaps dev/cephfs-snapshots |
| cephfs/fscrypt.rst | Fscrypt Encryption on CephFS | 4 File | Operate | mixed; overlaps dev/cephfs-fscrypt |
| cephfs/eviction.rst | Ceph file system client eviction | 4 File | Troubleshoot | concept plus procedure; Operate or Troubleshoot |
| cephfs/scrub.rst | Ceph File System Scrub | 4 File | Operate | |
| cephfs/damaged-rank.rst | Damaged Ranks | 4 File | Troubleshoot | |
| cephfs/full.rst | Handling a full Ceph file system | 4 File | Troubleshoot | |
| cephfs/disaster-recovery-experts.rst | Advanced: Metadata repair tools | 4 File | Troubleshoot | 529 lines |
| cephfs/troubleshooting.rst | Troubleshooting | 4 File | Troubleshoot | 597 lines; already symptom-led |
| cephfs/disaster-recovery.rst | Disaster recovery | 4 File | Troubleshoot | |
| cephfs/cephfs-journal-tool.rst | cephfs-journal-tool | 4 File | Reference | tool reference used by Troubleshoot; no man page |
| cephfs/recover-fs-after-mon-store-loss.rst | Recovering the file system after catastrophic Monitor store loss | 4 File | Troubleshoot | |
| cephfs/journaler.rst | Journaler | 4 File | Reference | stub (7 lines, confval); merge into mds-config-ref |
| cephfs/capabilities.rst | Capabilities in CephFS | 4 File | Learn | internals-leaning concept; index files it under Developer Guides; could be Door 7 |
| cephfs/api/index.rst | CephFS APIs | 4 File | Reference | stub hub |
| cephfs/api/libcephfs-py.rst | LibCephFS (Python) | 4 File | Reference | stub (automodule) |
| cephfs/api/libcephfs-java.rst | Libcephfs (Javadoc) | 4 File | Reference | stub; external link |
| cephfs/mantle.rst | Mantle | 4 File | Operate | experimental Lua balancer; developer-leaning; could be Door 7 |
| cephfs/experimental-features.rst | Experimental Features | 4 File | Reference | not in cephfs/index toctree; deprec; retire or fold into kernel-features |
| cephfs/metrics.rst | Metrics | 4 File | Reference | client and MDS metrics list |

### radosgw/ (76 pages, all Door 4 Object)

Also mapped into Object from elsewhere: cephadm/services/rgw.rst (Set up) and mgr/rgw.rst (Set up) for 78 in total. The index toctree is one flat list of 50 entries with no grouping.

| path | title | door | part | note |
|---|---|---|---|---|
| radosgw/index.rst | Ceph Object Gateway | 4 Object | Learn | landing; flat 50-entry toctree; rewrite with the five parts |
| radosgw/frontends.rst | HTTP Frontends | 4 Object | Reference | beast options; mixed Set up and Reference |
| radosgw/multisite.rst | Multi-Site | 4 Object | Set up | long (1602); mixed: realm, zonegroup and zone concepts plus many procedures (failover, migration); split |
| radosgw/zone-features.rst | Zone Features | 4 Object | Reference | |
| radosgw/placement.rst | Pool Placement and Storage Classes | 4 Object | Operate | mixed concept and procedure |
| radosgw/multisite-sync-policy.rst | Multisite Sync Policy | 4 Object | Operate | long (726); mixed concept, procedure and examples |
| radosgw/pools.rst | Pools | 4 Object | Learn | short; merge into placement |
| radosgw/config-ref.rst | Ceph Object Gateway Config Reference | 4 Object | Reference | confval generated |
| radosgw/admin.rst | Admin Guide | 4 Object | Operate | long (1033); radosgw-admin users, quotas, usage; mixed procedure and reference; overlaps man/8/radosgw-admin |
| radosgw/account.rst | User Accounts | 4 Object | Operate | mixed concept and procedure |
| radosgw/s3.rst | Ceph Object Gateway S3 API | 4 Object | Reference | hub with feature support table |
| radosgw/s3/commons.rst | Common Entities | 4 Object | Reference | API reference; deprec note |
| radosgw/s3/authentication.rst | Authentication and ACLs | 4 Object | Reference | API reference; deprec note |
| radosgw/s3/serviceops.rst | Service Operations | 4 Object | Reference | API reference |
| radosgw/s3/bucketops.rst | Bucket Operations | 4 Object | Reference | API reference; long (969) |
| radosgw/s3/objectops.rst | Object Operations | 4 Object | Reference | API reference |
| radosgw/s3/s3control.rst | S3 Control | 4 Object | Reference | API reference |
| radosgw/s3/cpp.rst | C++ S3 Examples | 4 Object | Reference | client SDK example; candidate for Door 7 or ceph.io |
| radosgw/s3/csharp.rst | C# S3 Examples | 4 Object | Reference | client SDK example |
| radosgw/s3/java.rst | Java S3 Examples | 4 Object | Reference | client SDK example |
| radosgw/s3/perl.rst | Perl S3 Examples | 4 Object | Reference | client SDK example |
| radosgw/s3/php.rst | PHP S3 Examples | 4 Object | Reference | client SDK example |
| radosgw/s3/python.rst | Python S3 Examples | 4 Object | Reference | client SDK example |
| radosgw/s3/ruby.rst | Ruby AWS::SDK Examples (aws-sdk gem ~>2) | 4 Object | Reference | client SDK example; outdated SDK major version |
| radosgw/iam.rst | Ceph Object Gateway IAM API | 4 Object | Reference | |
| radosgw/rgw-cache.rst | RGW Data Caching and CDN | 4 Object | Operate | index links it as rgw-cache.rst with the extension |
| radosgw/swift.rst | Ceph Object Gateway Swift API | 4 Object | Reference | hub plus feature table |
| radosgw/swift/auth.rst | Authentication | 4 Object | Reference | API reference |
| radosgw/swift/serviceops.rst | Service Operations | 4 Object | Reference | API reference |
| radosgw/swift/containerops.rst | Container Operations | 4 Object | Reference | API reference |
| radosgw/swift/objectops.rst | Object Operations | 4 Object | Reference | API reference |
| radosgw/swift/tempurl.rst | Temp URL Operations | 4 Object | Reference | API reference |
| radosgw/swift/tutorial.rst | Tutorial | 4 Object | Set up | client-side tutorial; short |
| radosgw/swift/java.rst | Java Swift Examples | 4 Object | Reference | client SDK example |
| radosgw/swift/python.rst | Python Swift Examples | 4 Object | Reference | client SDK example |
| radosgw/swift/ruby.rst | Ruby Swift Examples | 4 Object | Reference | client SDK example |
| radosgw/adminops.rst | Admin Operations | 4 Object | Reference | long (3169); Admin Ops REST API; generate from source if possible |
| radosgw/api.rst | librgw (Python) | 4 Object | Reference | stub (16 lines) |
| radosgw/nfs.rst | NFS | 4 Object | Set up | RGW export over NFS-Ganesha; 372 lines; overlaps mgr/nfs; cross-link from File (NFS) |
| radosgw/keystone.rst | Integrating with OpenStack Keystone | 4 Object | Set up | external |
| radosgw/barbican.rst | OpenStack Barbican Integration | 4 Object | Set up | external |
| radosgw/vault.rst | HashiCorp Vault Integration | 4 Object | Set up | external; 440 lines |
| radosgw/kmip.rst | KMIP Integration | 4 Object | Set up | external |
| radosgw/opa.rst | Open Policy Agent Integration | 4 Object | Set up | external; short |
| radosgw/keycloak.rst | Integrating Keycloak with RadosGW | 4 Object | Set up | external |
| radosgw/ldap-auth.rst | LDAP Authentication | 4 Object | Set up | external |
| radosgw/multitenancy.rst | RGW Multi-tenancy | 4 Object | Learn | mixed concept and procedure |
| radosgw/compression.rst | Compression | 4 Object | Operate | procedure |
| radosgw/encryption.rst | Encryption | 4 Object | Set up | mixed: SSE concepts plus configuration |
| radosgw/bucketpolicy.rst | Bucket Policies | 4 Object | Reference | policy grammar plus examples |
| radosgw/dynamicresharding.rst | RGW Dynamic Bucket Index Resharding | 4 Object | Operate | mixed concept, procedure and confval |
| radosgw/mfa.rst | RGW Support for Multifactor Authentication | 4 Object | Operate | |
| radosgw/sync-modules.rst | Sync Modules | 4 Object | Learn | hub plus concept |
| radosgw/archive-sync-module.rst | Archive Sync Module | 4 Object | Set up | short |
| radosgw/cloud-sync-module.rst | Cloud Sync Module | 4 Object | Set up | |
| radosgw/elastic-sync-module.rst | Elasticsearch Sync Module | 4 Object | Set up | external |
| radosgw/notifications.rst | Bucket Notifications | 4 Object | Operate | long (788); mixed concept, procedure and REST reference; deprec note; split |
| radosgw/s3-notification-compatibility.rst | S3 Bucket Notifications Compatibility | 4 Object | Reference | |
| radosgw/layout.rst | RADOS Gateway Data Layout | 4 Object | Learn | internals-leaning concept; could be Door 7 |
| radosgw/STS.rst | STS in Ceph | 4 Object | Set up | mixed concept, config and API examples |
| radosgw/STSLite.rst | STS Lite | 4 Object | Set up | deprec note |
| radosgw/session-tags.rst | Session tags for Attribute Based Access Control in STS | 4 Object | Reference | mixed |
| radosgw/role.rst | Role | 4 Object | Reference | long (604); REST API for roles |
| radosgw/oidc.rst | OpenID Connect Provider in RGW | 4 Object | Reference | REST API |
| radosgw/orphans.rst | Orphan List and Associated Tooling | 4 Object | Troubleshoot | tools; deprec note for radosgw-admin orphans |
| radosgw/troubleshooting.rst | Troubleshooting | 4 Object | Troubleshoot | 208 lines; symptom-led |
| radosgw/qat-accel.rst | QAT Acceleration for Encryption and Compression | 4 Object | Set up | hardware-specific |
| radosgw/uadk-accel.rst | UADK Acceleration for Compression | 4 Object | Set up | hardware-specific |
| radosgw/s3select.rst | Ceph s3 select | 4 Object | Reference | long (813); feature reference |
| radosgw/lua-scripting.rst | Lua Scripting | 4 Object | Reference | long (606); API reference plus examples |
| radosgw/d3n_datacache.rst | D3N RGW Data Cache | 4 Object | Set up | |
| radosgw/cloud-transition.rst | Cloud Transition | 4 Object | Operate | 523 lines; mixed |
| radosgw/cloud-restore.rst | Cloud Restore | 4 Object | Operate | |
| radosgw/metrics.rst | Metrics | 4 Object | Reference | perf counter list |
| radosgw/bucket_logging.rst | Bucket Logging | 4 Object | Operate | mixed procedure and reference |
| radosgw/s3_objects_dedup.rst | Full RGW Object Dedup | 4 Object | Operate | |

### csi/ (6 pages, all Door 4 Kubernetes)

| path | title | door | part | note |
|---|---|---|---|---|
| csi/index.rst | Ceph Container Storage Interface (CSI) | 4 Kubernetes | Learn | landing; already in the proposed shape (Learn, then Set up per backend); external with an explicit "where the documentation lives" scope statement |
| csi/deployment.rst | Deploying Ceph-CSI | 4 Kubernetes | Set up | external (operator, Helm, raw manifests); Helm and raw manifests marked deprecated |
| csi/rbd.rst | RBD with Ceph-CSI | 4 Kubernetes | Set up | Ceph-side preparation (pool, CephX user) |
| csi/cephfs.rst | CephFS with Ceph-CSI | 4 Kubernetes | Set up | Ceph-side preparation |
| csi/nfs.rst | NFS with Ceph-CSI | 4 Kubernetes | Set up | Ceph-side preparation |
| csi/nvmeof.rst | NVMe-oF with Ceph-CSI | 4 Kubernetes | Set up | short; under active development |

## Family maps

### rados/ (72 pages)

| Subdirectory | Pages | Door split | Notes |
|---|---|---|---|
| rados/configuration | 17 | 6 Reference (12), 3 Operate (5) | Reference: index (hub), auth-config-ref, bluestore-config-ref, filestore-config-ref (deprec, retire), general-config-ref (stub, 19), journal-ref (stub, 18), mclock-config-ref, mon-config-ref, mon-osd-interaction, network-config-ref, osd-config-ref, pool-pg-config-ref. Operate: ceph-conf (Configuring Ceph, long 782, mixed), common, mon-lookup-dns, msgr2, storage-devices (Learn). All *-ref pages use confval and are already source-generated |
| rados/operations (with pgcalc) | 34 | 3 Operate (27), 6 Reference (6), 5 Troubleshoot (1) | Reference: control (Control Commands, 700 lines), erasure-code-clay, -isa, -jerasure, -lrc, -shec (plugin parameter pages). Troubleshoot: health-checks (2391 lines, the health code catalogue). Operate: everything else; long mixed pages needing a split are crush-map (1193), placement-groups (1053), pools (917), monitoring (866), user-management (874), crush-map-edits (773), erasure-code (576); cache-tiering is deprecated and should retire; pg-concepts, pg-states, data-placement are Learn pages |
| rados/troubleshooting | 8 | 5 Troubleshoot (8) | index (hub), troubleshooting-mon (836), troubleshooting-osd (1020), troubleshooting-pg (938), log-and-debug, memory-profiling, cpu-profiling, community (get help). The three long pages are already problem-led and become the spine of the Door 5 hub |
| rados/api | 7 | 6 Reference (7) | index, librados (C), libradospp (stub, 9 lines), python, libcephsqlite, objclass-sdk, librados-intro (1052-line tutorial that fits Door 7 "build on Ceph" better than Reference) |
| rados/bluestore | 4 | 3 Operate (2), 6 Reference (2) | Operate: bluefs-spillover-cleaner, fast-onode-scan. Reference: fcm-plugin, rocksdb-config. Not linked from rados/index; reached from bluestore-config-ref |
| rados/man | 1 | 6 Reference | hub over man/8 (19 pages plus ceph-post-file hidden); dissolve |
| rados/index.rst | 1 | 3 Operate | landing with three columns (Config and Deploy, Operations, APIs); dissolves into Doors 3 and 6 |

### mgr/ (29 pages)

| Group | Pages | Door | Files |
|---|---|---|---|
| Orchestration | 3 | 3 Operate (1), 2 Deploy (1), 7 Develop (1) | orchestrator (Orchestrator CLI, Operate); rook (Deploy: Rook backend, 39 lines, stub-like); orchestrator_modules (Develop: writing orchestrator plugins) |
| Dashboard and APIs | 6 | 3 Operate (4), 6 Reference (2) | dashboard (1752 lines, mixed set up, operate and reference; split), dashboard_plugins/debug.inc, feature_toggles.inc, motd.inc (includes); ceph_api/index (RESTful API, Reference), cli_api (Reference) |
| Monitoring and alerting | 10 | 3 Operate | prometheus (470, mixed with confval), alerts, influx, telegraf, telemetry, crash, insights, iostat, diskprediction, progress |
| NFS, SMB and service modules | 4 | 4 Storage services | nfs (1242 lines, File NFS, overlaps cephadm/services/nfs and cephfs/nfs), smb (2084 lines, File SMB, overlaps cephadm/services/smb), rgw (Object Set up: realm bootstrap via mgr module), mds_autoscaler (File, stub 24 lines) |
| Misc | 6 | 3 Operate (4), 7 Develop (2) | administrator (ceph-mgr Administrator's Guide), index (hub), localpool, ceph_secrets (Operate); modules (module developer's guide, 881 lines) and hello (example module) to Develop |

Each module page mixes an operator guide with an option table (`.. mgr_module::` or confval); the option tables should be generated into Door 6 and the guide stay in Operate.

### man/ (51 pages, all Door 6 Reference; all `:orphan:`)

| Group | Pages | Files |
|---|---|---|
| Cluster daemons and core CLI | 7 | ceph (1879 lines), ceph-mon, ceph-osd, ceph-mds, ceph-run, ceph-syn, cephadm (664) |
| Keys, auth and config | 4 | ceph-authtool, ceph-create-keys, ceph-conf, librados-config |
| Maps and CRUSH | 4 | crushtool, crushdiff, monmaptool, osdmaptool |
| OSD and store tools | 10 | ceph-bluestore-tool, ceph-objectstore-tool, ceph-kvstore-tool, ceph-monstore-tool, ceph-volume (568), ceph-volume-systemd, ceph-dencoder, ceph-clsinfo, ceph-debugpack, ceph-post-file |
| RADOS | 2 | rados, ceph-immutable-object-cache |
| RBD | 10 | rbd (1072), rbd-fuse, rbd-nbd, rbd-ggate, rbdmap, ceph-rbdnamer, rbd-mirror, rbd-replay, rbd-replay-prep, rbd-replay-many |
| CephFS | 6 | ceph-fuse, mount.ceph, mount.fuse.ceph, cephfs-shell (652), cephfs-top, cephfs-mirror |
| RGW | 8 | radosgw, radosgw-admin (1095), rgw-orphan-list, rgw-gap-list, rgw-policy-check, rgw-policy-test, rgw-restore-bucket-index, ceph-diff-sorted |

Duplication with prose pages: man/8/rbd and rbd/rados-rbd-cmds; man/8/ceph and rados/operations/control; man/8/radosgw-admin and radosgw/admin; man/8/ceph-volume and ceph-volume/; man/8/cephfs-top and cephfs/cephfs-top; man/8/cephadm and cephadm/install plus cephadm/operations. Man pages are reached today through three hubs (man_index.rst, rados/man/index, rbd/man/index) and direct toctree entries in cephfs/index and radosgw/index.

### dev/ (154 pages, Door 7 Develop unless noted)

| Subdirectory | Pages | Notes |
|---|---|---|
| dev/developer_guide (with testing_integration_tests) | 19 | Contributor track: workflow, essentials, merging, tests, teuthology, dashboard developer docs (dash-devel, 2748 lines), jaegertracing (duplicates jaegertracing/index) |
| dev top-level files | 71 | Internals plus the user-facing candidates listed below |
| dev/osd_internals (with erasure_coding) | 31 | OSD internals and EC design documents |
| dev/crimson | 10 | Crimson and SeaStore internals |
| dev/cephadm (with design) | 7 | Design notes; linked from cephadm/index as "Cephadm Feature Planning" and from developer_guide; not user docs |
| dev/ceph-volume | 5 | ceph-volume developer notes |
| dev/mds_internals | 5 | MDS internals |
| dev/radosgw (with admin) | 5 | RGW internals; s3_compliance and admin/adminops_nonimplemented are user-facing reference |
| dev/dashboard | 1 | UI design goals |

dev/ pages that are user-facing or duplicate a user page, with the user door they belong to:

| dev page | User door | Reason |
|---|---|---|
| dev/ceph_krb_auth.rst | 3 Operate (security) or retire | 1096-line Kerberos set-up guide written for operators; the feature never shipped as supported |
| dev/perf_counters.rst, dev/perf_histograms.rst | 3 Operate (monitoring) plus 6 Reference | Admin socket perf dump is an operator task; schema is reference |
| dev/health-reports.rst | 3 Operate | "How to get reports" is operator content; implementation half stays in Door 7 |
| dev/crush-msr.rst | 3 Operate (CRUSH) | MSR rules are user-configurable; belongs beside rados/operations/crush-map |
| dev/mon-elections.rst | 3 Operate (Learn) | Concept behind rados/operations/change-mon-elections |
| dev/erasure-coded-pool.rst | 3 Operate | Overlaps rados/operations/erasure-code; merge |
| dev/config.rst | 3 Operate | Overlaps rados/configuration/ceph-conf; merge |
| dev/cephfs-mirroring.rst | 4 File | Duplicates cephfs/cephfs-mirroring (641 vs 1466 lines); merge |
| dev/cephfs-snapshots.rst, dev/cephfs-fscrypt.rst, dev/file-striping.rst | 4 File (Learn) | Concept pages that pair with cephfs/snapshots, cephfs/fscrypt, cephfs/file-layouts |
| dev/radosgw/s3_compliance.rst | 4 Object (Reference) | S3 API compliance table that users look for |
| dev/radosgw/admin/adminops_nonimplemented.rst | 4 Object (Reference) | Companion to radosgw/adminops |
| dev/rbd-diff.rst, dev/rbd-export.rst | 6 Reference | File format specs for tooling authors |
| dev/zoned-storage.rst | 2 Deploy (advanced) | Build and deploy notes for SMR devices; mixed |
| dev/dpdk.rst, dev/blkin.rst | 3 Operate plus 7 | Config half is operator content, build half is developer |
| dev/documenting.rst, dev/generatedocs.rst | 7 Develop | Correct door, but duplicate start/documenting-ceph; merge into one docs guide |
| dev/developer_guide/jaegertracing.rst | 7 Develop | Duplicates jaegertracing/index and cephadm/services/tracing |
| dev/cephadm/host-maintenance.rst, dev/cephadm/compliance-check.rst | 7 Develop | Design proposals; remove the "Feature Planning" link from cephadm user navigation |
| dev/kubernetes.rst, dev/dev_cluster_deployment.rst | 7 Develop | Explicitly not user docs; keep |
| dev/osd_internals/erasure_coding/client_support.rst | 7 Develop | Design doc; its user-facing facts (EC overwrites, omap on EC) belong in rados/operations/erasure-code |

### Small families and single files

| Family | Pages | Door | Notes |
|---|---|---|---|
| api/ | 2 | 6 Reference | index (API Documentation hub) and mon_command_api (3-line stub, generated at build) |
| releases/ | 22 | 6 Reference | general (cadence, naming, lifecycle; link from Door 1 and Door 2), index (timeline), 20 per-release notes from argonaut to tentacle (generated aggregates); changelog/ holds 69 historical .txt files |
| security/ | 14 | 7 Develop (4), 6 Reference (10) | index (Security), process, securitylead, workinggroup are project process; cves.rst plus 9 CVE pages are reference (CVE pages are reached only from cves.rst) |
| ceph-volume/ | 24 | 6 Reference | index and intro (deprec notes), inventory, drive-group (stub 14), systemd; lvm/ 13 subcommand pages (activate, batch, create, encryption, list, migrate, new-db, new-wal, prepare, scan stub, systemd, zap, index); simple/ 4 (legacy ceph-disk migration); zfs/ 2 (FreeBSD). Subcommand pages are reference; the one provisioning procedure operators need should live in Operate (OSD service) and link here |
| monitoring/ | 1 | 3 Operate | 507 lines: monitoring stack, then per-service metric sections (OSD, pool, RGW, CephFS, Block, hardware); Learn plus Reference; the service sections belong in each service's Operate part |
| hardware-monitoring/ | 1 | 3 Operate | 194 lines: overview, limitations, deploy the agent, examples, "For Developers" (Door 7) |
| jaegertracing/ | 1 | 3 Operate | 134 lines; overlaps cephadm/services/tracing and dev/developer_guide/jaegertracing |
| architecture/ | 9 | 1 Start here | index (hub), storage-cluster, scalability-high-availability, dynamic-cluster-management, erasure-coding, ceph-clients (Learn); ceph-protocol, extending-ceph (could be Door 7); cache-tiering (48 lines, deprec; retire) |
| crimson/ | 1 | 2 Deploy | Crimson (Tech Preview): deploy with cephadm, required flags, CPU allocation, backends, metrics; mixed |
| glossary.rst | 1 | 6 Reference | 582 lines |
| governance.rst | 1 | 7 Develop | |
| foundation.rst | 1 | 7 Develop | |
| technical-charter.rst | 1 | 7 Develop | |
| man_index.rst | 1 | 6 Reference | build-only toctree; 45 of 51 man pages |
| index.rst | 1 | 1 Start here | root landing; rewrite |

## Summary by door

Rule for the rewrite estimate. A page counts as "rewrite" if any of these hold: it is a hub or stub that dissolves into navigation; it clearly mixes concept with procedure (or procedure with reference) and must be split into the three page types; it is over about 600 lines, which under one-task-per-procedure forces a split; or it is deprecated content to retire. Every other page counts as "re-home only": it moves behind a redirect, gains the metadata block and a type label, and keeps its content. Generated reference (confval, mgr_module, automodule), man pages, release notes and Door 7 pages count as re-home only. The count is a reading of first headings, line counts and section structure, not a line-by-line edit estimate.

| Door | Existing pages mapped | Rewrite | Re-home only | Biggest ambiguities |
|---|---|---|---|---|
| 1 Start here | 13 | 5 | 8 | How deep architecture/ goes before it becomes internals; quick-rbd is stale and orphaned; where the Rook and Kubernetes introduction lives (Deploy or Start here) |
| 2 Deploy | 21 | 7 | 14 | Upgrades in Deploy (proposal) versus Operate; cephadm service pages for storage daemons; Windows client install (Deploy or the services); crimson tech preview placement |
| 3 Operate | 72 | 18 | 54 | mgr modules split three ways; monitoring content spread over five places; "security" collides with security/ (vulnerability process); health-checks home; cephadm/operations grab-bag |
| 4 Storage services | 190 (Block 43, File 63, Object 78, Kubernetes 6) | 44 | 146 | NFS and SMB pages scattered across cephadm, mgr, cephfs, radosgw, csi; iSCSI legacy footprint (13 pages); 10 RGW SDK example pages; Block has no Troubleshoot page; RGW index is a flat 50-entry list |
| 5 Troubleshoot | 11 | 5 | 6 | The hub is new; 11 more service troubleshooting pages stay in Door 4 and are linked; health-checks is both the symptom index and a reference table |
| 6 Reference | 141 | 8 | 133 | Man pages duplicate six prose pages; ceph-volume Deploy versus Reference; rados/api Reference versus Develop; release notes generation; changelog/ archive |
| 7 Develop and contribute | 168 | 3 | 165 | About 20 dev/ pages are user-facing; security process versus CVE list; three overlapping docs guides; cephadm design docs linked from user nav |
| Total | 616 | 90 | 526 | |

## Ambiguities and recommendations

1. mgr modules split across Operate, Reference and the services. Each module page is a guide plus an option table. Recommendation: one operator page per module in Door 3 (or in the service for nfs, smb, rgw, mds_autoscaler, snap-schedule), option tables generated into Door 6, module authoring (modules.rst, orchestrator_modules.rst, hello.rst) in Door 7, mgr/index dissolved. Rook (mgr/rook.rst) becomes the Door 2 "Rook and Kubernetes" entry, expanded.
2. ceph-volume as Deploy versus Reference. The 24 pages are subcommand references with a short intro. Recommendation: Door 6 Reference (CLI), with one Operate procedure "Provision OSDs with ceph-volume" under the OSD service page linking into it; mark simple/ (ceph-disk migration) and zfs/ as legacy; ceph-volume/intro merges with the man page synopsis.
3. hardware-monitoring. A single page mixing overview, limitations, a deploy procedure, examples and a developer section. Recommendation: Door 3 Operate > Monitoring, split into concept plus procedure; the "For Developers" section goes to Door 7; consider folding into the monitoring landing so hardware, Prometheus stack and SNMP sit together.
4. Man pages that duplicate reference pages. rbd, ceph, radosgw-admin, ceph-volume, cephfs-top and cephadm each have both a man page and a prose page covering the same commands. Recommendation: man pages are the single CLI reference in Door 6 (generated into JSON per Move 3); prose pages keep procedures and link to the man page for options; retire rbd/man/index and rados/man/index hubs; add the six man pages missing from man_index.rst.
5. dev/ pages that are user-facing. About 20 pages (listed in the dev family map) carry operator content: Kerberos set-up, perf counters and histograms, CRUSH MSR, health reports, config system, CephFS mirroring and snapshots concepts, S3 compliance, RBD file formats. Recommendation: move the operator halves into Doors 3, 4 and 6 during each section's rebuild and leave design halves in Door 7; drop the "Cephadm Feature Planning" link from cephadm/index so design proposals stop appearing in user navigation.
6. health-checks.rst (2391 lines). It is the health-code catalogue and the natural spine of a symptom-organized Door 5. Recommendation: generate the code table into Door 6 from source, and build the Door 5 hub as symptom pages that link codes to the existing rados, cephfs, radosgw and cephadm troubleshooting pages; keep the service troubleshooting pages inside Door 4 so each service stays self-contained.
7. architecture/ depth. Recommendation: Door 1 Learn keeps storage-cluster, scalability-high-availability, dynamic-cluster-management, erasure-coding and ceph-clients; ceph-protocol and extending-ceph move to Door 7 internals; cache-tiering retires with rados/operations/cache-tiering.
8. Two meanings of "security". The proposal's Operate door lists security (cephx, users, certificates), while the security/ directory is the vulnerability process and CVE list. Recommendation: Operate > Security gathers rados/operations/user-management, rados/configuration/auth-config-ref, cephadm/certmgr, oauth2-proxy and mgmt-gateway; security/index, process, securitylead and workinggroup go to Door 7; cves.rst and the CVE pages go to Door 6 with a link from Door 2 upgrades.
9. cephadm/services pages for storage daemons. mds, rgw, nfs, smb and iscsi are deployment procedures for a service, written from cephadm's point of view. Recommendation: they become the Set up part of each service (with a service-spec reference in Door 6); mon, mgr, osd, monitoring, snmp-gateway, mgmt-gateway, oauth2-proxy, tracing and custom-container stay in Door 3.
10. Upgrades. cephadm/upgrade, cephfs/upgrading, rados/operations/require-osd-release, require-min-compat-client and the upgrade notes inside releases/*.rst are five places. Recommendation: Door 2 > Upgrade hub (as the proposal puts upgrades in Deploy) with one procedure per path and the service-specific steps included from the services.
11. NFS and SMB. NFS spans cephadm/services/nfs, mgr/nfs (1242 lines), cephfs/nfs, radosgw/nfs and csi/nfs; SMB spans cephadm/services/smb and mgr/smb (2084 lines). Recommendation: File > NFS and File > SMB sub-services each in the five-part shape, built from the mgr and cephadm pages; radosgw/nfs stays under Object with a cross-link (or is marked legacy); csi/nfs stays in Kubernetes.
12. iSCSI gateway. 13 pages plus cephadm/services/iscsi for a gateway in maintenance mode. Recommendation: Block > Gateways with NVMe-oF first and iSCSI marked legacy; retire iscsi-target-ansible; collapse the three hub pages.
13. RGW SDK examples. Ten language example pages (seven S3, three Swift), several against outdated SDK versions. Recommendation: keep one "client examples" reference page per API in Object > Reference and move the per-language pages to ceph.io or an examples repo; do not carry them into the template unchanged.
14. rados/api. librados-intro is a 1052-line tutorial for application developers, the rest are API references. Recommendation: API references (C, C++, Python, sqlite, objclass) to Door 6, generated where automodule allows; librados-intro to Door 7 as "Build applications on Ceph".
15. releases/general. Cadence and lifecycle are what a new reader needs to choose a release. Recommendation: Door 6 keeps the page; Door 1 gets a short "Which release should I run" concept that links to it.
16. crimson. A tech-preview deployment page whose internals live in dev/crimson. Recommendation: Door 2 > Advanced deployments with a tech-preview banner; flags and metrics sections become Reference stubs; dev/crimson stays in Door 7.
17. Windows client pages. install/windows-install, windows-basic-config and windows-troubleshooting are orphans; rbd/rbd-windows and cephfs/ceph-dokan cover the same clients. Recommendation: Door 2 > Clients > Windows for install and config, the service pages keep mapping and mounting, windows-troubleshooting joins Door 5.
18. Monitoring spread. monitoring/index, cephadm/services/monitoring, mgr/prometheus, mgr/alerts and the per-service metrics pages (radosgw/metrics, cephfs/metrics, rbd iscsi-monitoring) are five homes. Recommendation: Door 3 > Monitoring landing owns the stack (deploy, Prometheus module, alerts, SNMP, hardware); each service's Operate part owns its metrics page; monitoring/index's per-service sections move to the services.
19. Tracing. jaegertracing/index, cephadm/services/tracing and dev/developer_guide/jaegertracing describe the same setup. Recommendation: one Operate page (deploy and enable tracing) and one Door 7 page (instrumenting code).
20. start/quick-rbd. Reachable only from an iSCSI page, written for pre-cephadm clusters. Recommendation: rewrite as the Door 1 block quick start on top of cephadm, or retire in favour of the Block Set up procedures.
21. Dashboard. mgr/dashboard.rst is 1752 lines and a root toctree entry. Recommendation: Door 3 > Dashboard with three pages (set up and SSO, operate, feature reference); the 2748-line dash-devel stays in Door 7.
22. Naming and orphan hygiene found during the mapping: cephfs/standby.rst has no document title; radosgw/index links rgw-cache.rst with its extension; cephfs/experimental-features.rst is not in any toctree; the three .inc.rst files under mgr/dashboard_plugins are includes and must not be given metadata blocks of their own.

## Reusable as-is

- csi/ already has the proposed shape: a Learn landing with a scope statement, then one Set up page per backend that prepares the Ceph side and links to canonical Ceph-CSI docs. Reuse it as the model for the Kubernetes service and for how to write external-integration pages.
- cephfs/index.rst already groups its toctrees as Administration, Mounting, Concepts, Troubleshooting and Disaster Recovery, and Developer Guides. The headings are hidden inside raw HTML comments; un-hiding and renaming them to Learn, Set up, Operate, Troubleshoot, Reference gives the File service its navigation without moving files.
- rados/ is already split by door: configuration/ (Reference), operations/ (Operate), troubleshooting/ (Troubleshoot), api/ (Reference). The Door 3, 5 and 6 toctrees can point at these directories directly in the navigation-layer phase.
- rbd/index.rst hubs (Basic Commands, Operations, Integrations, Manpages, APIs) map onto Set up, Operate, Set up (integrations), Reference, Reference. The Operations and Integrations toctrees can be relabeled rather than rebuilt.
- install/index.rst is already a deployment-method chooser (cephadm, Rook, other tools, manual, Windows) and can be the Door 2 landing with light edits.
- cephadm/ already separates install, adoption, upgrade, operations and troubleshooting; only services/ and operations.rst need splitting.
- rados/troubleshooting/index and the three long troubleshooting pages (mon, osd, pg) are already problem-led and form the first draft of the Door 5 hub; cephfs/troubleshooting and radosgw/troubleshooting are also symptom-led.
- Generated reference is already in place for Door 6: confval directives in rados/configuration/*-ref, rbd/rbd-config-ref, cephfs/mds-config-ref and client-config-ref, radosgw/config-ref, mgr module option tables via mgr_module, automodule API pages, and the man pages built from man_index.rst. Move 3's JSON export can start from these sources without rewriting prose.
- releases/index.rst and security/cves.rst are already reference lists; glossary.rst is complete as a Door 6 page.
- dev/developer_guide/index.rst and dev/internals.rst already form the two Door 7 tracks (contribute, internals) and need only re-homing plus the extraction of the user-facing pages listed above.
- architecture/index.rst toctree order (storage cluster, scalability, dynamic management, erasure coding, clients) already reads as a Learn track for Door 1.


---

[Back to the proposal](../)
