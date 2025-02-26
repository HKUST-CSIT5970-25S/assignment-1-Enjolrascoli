[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)

# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Jiang Zhihui

### Student Id: 21072458

### Email: zjiangbi@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose _any_ open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

   > The tool used is `sysbench`.
   > For cpu, the command is `sysbench --cpu-max-prime=20000 --threads=$(nproc) cpu run`.
   > For memory, the command is `sysbench --threads=$(nproc) memory run`

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

   In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

   | Size        | CPU performance | Memory performance |
   | ----------- | --------------- | ------------------ |
   | `t2.micro`  | 895.85          | 538.58MiB/sec      |
   | `t2.medium` | 1651.56         | 916.49 MiB/sec     |
   | `c5d.large` | 701.65          | 7534.61 MiB/sec    |

   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

   | Type                      | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | `t3.medium` - `t3.medium` | 25800          | 0.033    |
   | `m5.large` - `m5.large`   | 33800          | 0.021    |
   | `c5n.large` - `c5n.large` | 36700          | 0.022    |
   | `t3.medium` - `c5n.large` | 4600           | 0.758    |
   | `m5.large` - `c5n.large`  | 4950           | 0.529    |
   | `m5.large` - `t3.medium`  | 1770           | 0.973    |

   > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

   | Connection                | TCP b/w (Mbps) | RTT (ms) |
   | ------------------------- | -------------- | -------- |
   | N. Virginia - Oregon      | 470            | 60.912   |
   | N. Virginia - N. Virginia | 47800          | 0.138    |
   | Oregon - Oregon           | 47800          | 0.199    |

   > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
