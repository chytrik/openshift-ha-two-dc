# OpenShift Two-DC Explorer

Interactive guide to running **Red Hat OpenShift with high availability across two data centers**: why one cluster stretched over two sites does not survive the loss of either site, which architecture options exist, and which one fits a given RPO, data placement and workload mix.

**Live demo:** https://chytrik.github.io/openshift-ha-two-dc/

Languages: Čeština (default) · Slovenčina · Polski · Română · English

---

> [!IMPORTANT]
> **Current as of 18 October 2026.**
> This is informational demo material. It is **not an official Red Hat publication, product documentation or support statement**. Product capabilities, support status (Technology Preview vs. GA), latency limits and subscription terms change between releases. Before using any statement in an architecture decision, verify it against the current Red Hat documentation and with your Red Hat account team.
>
> RPO and RTO values shown in the app are typical ranges taken from the sources below, not guarantees. Measure them in your own failover test. The configurator is a decision aid for discovery conversations, not an architecture or sizing sign-off.

> [!NOTE]
> **Upozornění (CZ):** Stav k 18. 10. 2026. Jde o informativní demo, nikoli o oficiální dokumentaci nebo stanovisko podpory Red Hat. Možnosti produktů, stav podpory (Technology Preview / GA), limity latence a podmínky subskripcí se mezi verzemi mění; před architektonickým rozhodnutím vše ověřte v aktuální dokumentaci Red Hat a s account týmem. Hodnoty RPO/RTO jsou typické rozsahy, ne záruky.

---

## What the app covers

| Section | What you can do |
| --- | --- |
| The problem | etcd quorum simulator: pick a topology (2+1, 1+1+1, 2+2, 3+2, two clusters), fail a site or cut the DC1–DC2 link, and see what happens to the API, workloads and recovery. Plus HA vs. DR, "DR is two problems", the disposable cluster principle and blast radius. |
| Options | Seven architecture options A–G with details, an RPO/RTO map and a side-by-side table. |
| Configurator | Six inputs (where stateful data live, required RPO, third site, latency between DCs, platform, single-cluster requirement) produce a recommended option, what to combine it with, warnings and prerequisites. |
| Data & storage, Traffic, Management, Virtualization | ODF stretch / Metro-DR / Regional-DR, storage arrays, application replication, backups; GSLB and Connectivity Link; ACM hub resilience and GitOps; OpenShift Virtualization specifics. |
| Discovery | Checklist of questions for the customer (state is kept in the browser). |
| Sources | Links to the documentation and articles the content is based on. |

## What the content is based on

Product versions referenced:

| Area | Version referenced |
| --- | --- |
| OpenShift Container Platform (etcd guidance for spanned clusters, quorum restoration, 4–5 control plane nodes, Two-Node with Arbiter) | 4.17–4.22 documentation |
| OpenShift Data Foundation (stretch cluster, Metro-DR, Regional-DR) | 4.18 |
| Red Hat Advanced Cluster Management (hub backup and restore) | 2.7+ |
| Red Hat Connectivity Link (CoreDNS for on-prem DNS) | 1.3 |
| OpenShift Virtualization (cross-cluster live migration, Tech Preview) | 4.20 |

Red Hat documentation:

- [OCP 4.21 — Guidance for clusters that span data centers](https://docs.redhat.com/en/documentation/openshift_container_platform/4.21/html/etcd/etcd-guidance-span)
- [Restoring etcd quorum for high availability clusters (docs source)](https://github.com/openshift/openshift-docs/blob/main/modules/dr-restoring-etcd-quorum-ha.adoc)
- [Node scaling for etcd (docs source)](https://github.com/openshift/openshift-docs/blob/main/modules/etcd-node-scaling.adoc)
- [Two-Node with Arbiter (docs source)](https://github.com/openshift/openshift-docs/blob/main/installing/installing_two_node_cluster/about-two-node-arbiter-installation.adoc)
- [ODF 4.18 — Disaster recovery with stretch cluster](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.18/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/introduction-to-stretch-cluster-disaster-recovery_stretch-cluster)
- [ODF 4.18 — Metro-DR solution](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.18/html/configuring_openshift_data_foundation_disaster_recovery_for_openshift_workloads/metro-dr-solution)
- [ODF 4.18 — Planning your deployment: Disaster Recovery](https://docs.redhat.com/en/documentation/red_hat_openshift_data_foundation/4.18/html/planning_your_deployment/disaster-recovery)
- [Red Hat Connectivity Link 1.3 — release notes](https://docs.redhat.com/en/documentation/red_hat_connectivity_link/1.3/html/whats_new/rhcl-release-notes)
- Knowledgebase (subscriber access): [3220991 — Deployments Spanning Multiple Sites](https://access.redhat.com/articles/3220991), [3221001 — HA and Recommended Practices](https://access.redhat.com/articles/3221001)

Red Hat blog posts and articles:

- [A Guide to High Availability/Disaster Recovery for Applications on OpenShift](https://www.redhat.com/en/blog/a-guide-to-high-availability/disaster-recovery-for-applications-on-openshift) — Santosh Gurijala, Andrew Sullivan
- [Disaster Recovery Strategies for Applications Running on OpenShift](https://www.redhat.com/en/blog/disaster-recovery-strategies-for-applications-running-on-openshift) — Raffaele Spazzoli
- [Deploying OpenShift Applications to Multiple Datacenters](https://www.redhat.com/en/blog/deploying-openshift-applications-multiple-datacenters) — Raffaele Spazzoli
- [Disaster recovery approaches for Red Hat OpenShift Virtualization](https://www.redhat.com/en/blog/disaster-recovery-approaches-red-hat-openshift-virtualization) and [part 2](https://developers.redhat.com/articles/2025/08/11/disaster-recovery-approaches-red-hat-openshift-virtualization-part-2)
- [How RHOCP 4.17 enhances control plane resilience](https://developers.redhat.com/articles/2025/02/12/how-rhocp-417-enhances-control-plane-resilience) — Mark Schmitt
- [Protecting virtual machines from storage and secondary network node failures](https://developers.redhat.com/articles/2025/10/13/protecting-virtual-machines-storage-and-secondary-network-node-failures) — Raffaele Spazzoli
- [Multicluster resiliency with global load balancing and mesh federation](https://developers.redhat.com/articles/2025/08/28/multicluster-resiliency-global-load-balancing-and-mesh-federation) — Raffaele Spazzoli
- [What's new in Red Hat OpenShift Virtualization 4.20](https://www.redhat.com/en/blog/whats-new-in-red-hat-openshift-virtualization-4.20)
- [Backup and restore hub clusters with Red Hat Advanced Cluster Management](https://www.redhat.com/en/blog/backup-and-restore-hub-clusters-with-red-hat-advanced-cluster-management-for-kubernetes)
- [Event-driven disaster recovery](https://www.redhat.com/en/blog/event-driven-disaster-recovery)

Regulation: [DORA, Article 12](https://www.springlex.eu/en/packages/dora/dora-regulation/article-12/) (backup, restoration and testing).

## Run locally

The whole app is a single `index.html` with no build step and no backend. Open it in a browser, or serve the folder:

```bash
python3 -m http.server 8080
# open http://localhost:8080
```

Fonts load from Google Fonts; without internet the app falls back to system fonts. The selected language, configurator answers and checklist state are stored in the browser's `localStorage` only.


