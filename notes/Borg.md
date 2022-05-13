# Borg

- [[Google]]의 인하우스 클러스터 관리 시스템

- [[Kubernetes]] 설계의 많은 부분이 Borg의 디자인을 모티브로 함

- [Large-scale cluster management at Google with Borg](https://research.google/pubs/pub43438/)
  - [[Google]]'s Borg system is a cluster manager that runs hundreds of thousands of jobs, from many thousands of different applications, across a number of clusters each with up to tens of thousands of machines.
  - It achieves high utilization by combining admission control, efficient task-packing, over-commitment, and machine sharing with process-level performance isolation. It supports high-availability applications with runtime features that minimize fault-recovery time, and scheduling policies that reduce the probability of correlated failures. Borg simplifies life for its users by offering a declarative job specification language, name service integration, real-time job monitoring, and tools to analyze and simulate system behavior.
  - We present a summary of the Borg system architecture and features, important design decisions, a quantitative analysis of some of its policy decisions, and a qualitative examination of lessons learned from a decade of operational experience with it.
