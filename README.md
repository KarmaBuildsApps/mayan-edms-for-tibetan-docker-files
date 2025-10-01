Documentation of Mayan EDMS for Tibetan 

Mayan EDMS is a free and open-source electronic document management system (EDMS) for storing, organizing, and retrieving digital documents

. It is built using Python and the Django framework and is known for its scalability, robust security, and advanced features like workflow automation, version control, and a REST API for integration.

## Hardware specs:

|**Component** |**Function in Docker**|**Specification**|**Rationale**|
| :-: | :-: | :-: | :-: |
|**Processor (CPU)**|A high-core-count, high-clock-speed server-grade CPU (e.g., AMD EPYC, Intel Xeon). A minimum of **16 cores** is recommended to handle concurrent OCR jobs, Elasticsearch indexing, and other background tasks.|OCR is heavily dependent on CPU performance. More cores allow more OCR worker containers to run in parallel without slowing down other services.|OCR is a CPU and memory-intensive task. Running multiple worker containers in parallel on powerful hardware allows for faster, more scalable processing.|
|**Memory (RAM)**|**64 GB or more** of ECC RAM.|This high amount of RAM is needed for multiple reasons:|Distributes the indexing and query load for thousands of books, ensuring high performance and redundancy.|
|||• The Elasticsearch container requires significant memory for its Java heap, with Elastic recommending 50% of the host RAM up to 30 GB per node.|Manages all application logic, schedules tasks for workers, and serves the user interface.|
|||• The OCR process itself consumes memory, especially for large, high-resolution book pages.|Separates the raw document storage from the fast, temporary storage used by OCR workers, preventing I/O bottlenecks.|
|||• The other Mayan EDMS services (PostgreSQL, Redis) also require RAM to function efficiently.|Ensures optimal performance for database transactions and fast indexing/query speeds for Elasticsearch.|
|**Storage (Primary)**|**2 TB or more** of high-performance NVMe SSDs|NVMe SSDs offer the best I/O performance, which is critical for both the PostgreSQL database (metadata) and Elasticsearch indices. |Critical for high-volume data transfer between the Mayan EDMS app, OCR workers, and Elasticsearch nodes.|


## Software requirements:
- **Operating System:** A stable, enterprise-grade Linux distribution with strong, native support for Docker. Recommended choices include Ubuntu Server (LTS version) or Debian.
- **Docker Engine:** This is the lightweight, command-line-based core container runtime required on the Linux server. It is different from Docker Desktop and offers better performance by avoiding the overhead of a virtual machine.
- **Docker Compose:** This tool is used to define and orchestrate the multi-container Mayan EDMS application from a single YAML file.
- **Containers:** All services for Mayan EDMS will run inside their own Docker containers, as defined in the *docker-compose.yml* file.
- **Git:** You must install Git on the server to clone the Mayan EDMS repository and get the necessary *docker-compose.yml* file. This allows you to easily pull updates in the future.










## Setup Instructions:
### Pull the Mayan EDMS

Command
```sh
    git clone https://github.com/KarmaBuildsApps/mayan-edms-for-tibetan-docker-files.git mayan-edms-tibetan
    cd mayan-edms-tibetan
```

### Assign IP Address
To restrict access to the internal network, we use nginx. For the server to be available via nginx:

- Navigate to the nginx configuration folder *mayan-edms-tibetan/nginx*
- Open nginx.conf and set the server’s IP address next to server\_name in the config file.

## Run Docker Compose
### Build and start the containers with:

Command:
```sh
    docker compose up -d --build
```
