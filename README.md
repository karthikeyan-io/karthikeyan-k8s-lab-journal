# 🧪 Karthikeyan's Kubernetes Lab Journal

> **CKA Preparation Journal** — Daily hands-on kubectl practice, YAML labs, troubleshooting scenarios and cluster architecture notes by a 19-year Telecom/IMS/NFV engineer transitioning into Cloud & AI engineering in Tokyo, Japan.

---

## 👤 About Me

| | |
|---|---|
| **Name** | Karthikeyan Ramamurthy |
| **Role** | Associate Consultant — Telecom Cloud & NFV @ HCL Tech Japan Ltd |
| **Location** | Tokyo, Japan 🇯🇵 |
| **Background** | 19+ years in Telecom · IMS · NFV · Nokia CloudBand · VoLTE · 5G Core |
| **Target** | AWS Japan Solutions Architect (Principal level) · 2026 |
| **LinkedIn** | [linkedin.com/in/karthikeyanramamurthy](https://www.linkedin.com/in/karthikeyanramamurthy/) |

---

## 🎯 Why This Repository Exists

I am preparing for the **CKA (Certified Kubernetes Administrator)** exam — targeting a **September 2026** pass date — while working full time as a cloud consultant in Tokyo.

This journal documents every lab session, every broken cluster I fixed, every kubectl command I drilled until it became muscle memory. It is a living record of deliberate practice, not polished tutorials.

If you are studying for CKA, this is the real picture of what daily preparation looks like — including the sessions that did not go smoothly.

---

## 📅 Study Plan

| Phase | Period | Focus |
|---|---|---|
| ✅ Week 1–2 | Jul 1–13 | Cluster Architecture · kubeadm · Static Pods · etcd |
| ✅ Week 3–4 | Jul 14–27 | Services · Networking · Network Policies · Ingress |
| ✅ Week 5–6 | Jul 28–Aug 10 | Storage · PV/PVC · Troubleshooting Part 1 |
| 🔄 Week 7–8 | Aug 11–24 | Troubleshooting Part 2 · killer.sh Simulator #1 |
| ⏳ Week 9 | Aug 25–31 | killer.sh Simulator #2 · Final polish · PSI setup |
| 🎯 **EXAM** | **Sep 2026** | **CKA Exam — Target: PASS first attempt** |

---

## 📂 Repository Structure

```
karthikeyan-k8s-lab-journal/
│
├── week-01/          # Cluster Architecture + kubeadm setup
│   ├── README.md     # Week summary + what I learned
│   ├── labs/         # YAML files and kubectl commands practised
│   └── notes.md      # Key concepts + gotchas
│
├── week-02/          # Workloads & Scheduling
│   ├── README.md
│   ├── labs/
│   └── notes.md
│
├── week-03/          # Services & Networking Part 1
├── week-04/          # Networking Part 2 + Storage
├── week-05/          # Troubleshooting Part 1
├── week-06/          # NAT-TEST week + Troubleshooting Part 2
├── week-07/          # Full Review + exam booked
├── week-08/          # killer.sh Simulator #1 + gap analysis
├── week-09/          # killer.sh Simulator #2 + final polish
│
├── scenarios/        # Reusable troubleshooting scenario bank
│   ├── crashloopbackoff.md
│   ├── imagepullbackoff.md
│   ├── node-notready.md
│   ├── pvc-pending.md
│   └── network-policy-debug.md
│
├── cheatsheet.md     # My personal kubectl quick-reference
└── README.md         # This file
```

---

## 🔧 Lab Environment

| Component | Tool |
|---|---|
| Local cluster | minikube / kind (Kubernetes in Docker) |
| Practice platform | KodeKloud CKA course labs |
| Exam simulator | killer.sh (2 sessions included with CKA voucher) |
| Reference | [kubernetes.io/docs](https://kubernetes.io/docs) (allowed in real exam) |
| OS | Ubuntu 22.04 |

---

## 📊 CKA Exam Domain Coverage

```
Troubleshooting                    ████████████████████████████████  30% ← highest priority
Cluster Architecture & Config      ████████████████████████          25%
Services & Networking              ████████████████████              20%
Workloads & Scheduling             ████████████                      15%
Storage                            ████████                          10%
```

---

## 🧠 My Telco → Kubernetes Mental Model

Coming from 13 years at Nokia Networks building IMS/VoLTE/NFV infrastructure, I map Kubernetes concepts to telco equivalents to accelerate understanding:

| Kubernetes Concept | Telco Equivalent (Nokia/IMS) |
|---|---|
| Pod | VNF instance (Virtual Network Function) |
| Deployment | VNF lifecycle manager (CBAM) |
| Service (ClusterIP) | Internal VLAN / IMS node routing |
| Ingress | SBC / Session Border Controller |
| Network Policy | Firewall ACL between IMS nodes |
| PersistentVolume | SAN/NAS storage for HSS subscriber data |
| Namespace | Network slice / VNF tenant |
| etcd | Network configuration database |
| kubeadm | Nokia CloudBand CBIS installer |
| kubectl | Nokia NetAct CLI equivalent |

> This mapping made complex Kubernetes concepts click immediately. If you have a networking or telco background, thinking this way dramatically reduces the learning curve.

---

## ⚡ Personal kubectl Cheatsheet Highlights

```bash
# Quick aliases — set these in ~/.bashrc before the exam
alias k=kubectl
alias kgp='kubectl get pods'
alias kgs='kubectl get svc'
alias kgn='kubectl get nodes'
export do='--dry-run=client -o yaml'   # generate YAML without applying
export now='--force --grace-period 0'  # force delete immediately

# Generate YAML skeleton instead of writing from scratch (exam time saver)
k run nginx --image=nginx $do > pod.yaml
k create deployment myapp --image=nginx --replicas=3 $do > deploy.yaml
k create service clusterip mysvc --tcp=80:80 $do > svc.yaml

# Troubleshooting reflex — always start here
k describe pod <pod-name>          # What is the event saying?
k logs <pod-name> --previous       # Crashed? Check previous container logs
k exec -it <pod-name> -- /bin/sh   # Get inside the container

# etcd backup — this WILL appear in the exam
ETCDCTL_API=3 etcdctl snapshot save /backup/etcd.db \
  --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key
```

---

## 📈 Weekly Progress Log

| Week | Topic | Hours | Key Win | Blocker |
|---|---|---|---|---|
| Week 1 | Cluster Architecture | 11 | kubeadm bootstrap from memory | etcd TLS flags — confusing at first |
| Week 2 | Workloads + TCJ starts | 10 | Rolling updates + rollbacks automatic | DaemonSet vs StatefulSet use cases |
| Week 3 | Networking Part 1 | 10 | NetworkPolicy from scratch in <5 min | CoreDNS resolution debugging |
| Week 4 | Networking + Storage | 11 | PVC bound to StorageClass first try | Ingress controller installation steps |
| Week 5 | Troubleshooting Pt 1 | 12 | CrashLoopBackOff fixed in 4 min | — |
| Week 6 | Troubleshoot + NAT-TEST | 7 | NAT-TEST sitting ✅ | Reduced study week intentionally |
| Week 7 | Review + exam booked | 11 | kubectl speed 50 commands timed | — |
| Week 8 | killer.sh #1 | 10 | Gap list identified clearly | — |
| Week 9 | killer.sh #2 + final | 8 | — | — |

---

## 🗾 The Tokyo Context

Studying for CKA in Tokyo while:
- Working full time as Associate Consultant at HCL Tech Japan Ltd
- Attending TCJ Japanese language school 3 evenings/week (Tue/Wed/Thu 7–9PM)
- Swimming 3×/week (Mon/Fri/Sat)
- Studying Japanese on the commute daily (Anki + JapanesePod101)
- Targeting JLPT N5 (December 2026) and NAT-TEST (August 2026)

**Study time breakdown per day:**
- 🚃 Commute (both ways): 1 hr — theory, notes review, short video clips
- 🏢 Office (break/lunch): 1 hr — KodeKloud videos, docs reading
- 🌙 Saturday deep lab: 2+ hrs — hands-on cluster work

**Total weekly CKA hours: ~10–12 hrs** alongside full-time work and Japanese study.

---

## 🔗 Related Repositories

| Repo | Description | Status |
|---|---|---|
| [karthikeyan-k8s-lab-journal](https://github.com/karthikeyan-io/karthikeyan-k8s-lab-journal) | This repo — CKA prep journal | 🟢 Active |
| telco-to-aws-architecture | IMS/VoLTE → AWS reference architectures | ⏳ Starting Sep 2026 |
| aws-sa-study-architectures | Well-Architected scenarios + ADRs | ⏳ Starting Oct 2026 |
| genai-telco-demo | RAG demo: Query 3GPP specs with AWS Bedrock | ⏳ Starting Jan 2027 |

---

## 📜 Certification Roadmap

```
2026
 Jul ──── CKA prep (this repo) ──────────────────────────────────┐
 Aug ──── NAT-TEST ✅                                             │
 Sep ──── 🎯 CKA EXAM ──────────────────────────────────────────►│
 Oct ──── 🎯 AWS SAA EXAM ─────────────────────────────────────► │
 Dec ──── JLPT N5                                                 │
2027                                                              │
 Mid ──── AWS ML Specialty ──────────────────────────────────────┤
 Jul ──── JLPT N4                                                 │
2028                                                              │
 ──────── AWS SAP + JLPT N3 ─────────────────────────────────────┘
```

---

## 🤝 Connect

I write weekly on LinkedIn about this journey — CKA labs, learning Japanese in Tokyo, the telco-to-cloud transition, and what it's like to reinvent your career at 42 in one of the world's most exciting tech markets.

**If you are:**
- Studying for CKA and want to compare notes
- A cloud engineer in Tokyo (foreign or Japanese)
- Working in telco and curious about the cloud transition
- Learning Japanese alongside a technical career

👉 **[Connect with me on LinkedIn](https://www.linkedin.com/in/karthikeyanramamurthy/)**

---

## 📄 License

This repository is open for reference and learning. All lab notes, YAML files, and scenarios are my own original work. Feel free to use them for your own CKA preparation.

---

<div align="center">

**Built in Tokyo 🗼 | Studying Kubernetes ☸️ | Learning Japanese 🇯🇵 | Targeting AWS Japan 🟠**

*"19 years in telecom taught me that infrastructure reliability is life-critical. That same discipline now drives how I learn cloud."*

![Tokyo](https://img.shields.io/badge/Based_in-Tokyo_Japan-red?style=flat-square)
![CKA](https://img.shields.io/badge/CKA-In_Progress-blue?style=flat-square&logo=kubernetes)
![AWS](https://img.shields.io/badge/AWS_SAA-Planned_Oct_2026-orange?style=flat-square&logo=amazon-aws)
![JLPT](https://img.shields.io/badge/JLPT-N5_Dec_2026-green?style=flat-square)
![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin)

</div>
