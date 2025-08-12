# Spark + Jupyter in Docker

This repository provides a **Dockerized environment for Apache Spark with Jupyter Notebook integration**, making it easy to develop, test, and run Spark applications locally or in a containerized setup.

## 🚀 Features

- **Jupyter Notebook** with root access and persistent workspace
- **Apache Spark 4.0.0**
  - Spark Master with web UI exposed
  - Spark Worker nodes connected automatically
- Shared **data volume** for exchanging files between Jupyter and Spark
- Pre-configured networking with an external Hadoop cluster (via `docker-hadoop_default` network)
- Ready-to-use environment with minimal setup

## 📦 Services

| Service        | Description                                   | Ports              |
|----------------|-----------------------------------------------|-------------------|
| `jupyter`      | Jupyter Notebook with Spark access            | configured by token |
| `spark-master` | Spark Master node with web UI                 | `9090` (UI), `7077` |
| `spark-worker` | Spark Worker node connected to Spark Master   | N/A               |

## 🛠 Prerequisites

- [Docker](https://www.docker.com/get-started)  
- [Docker Compose](https://docs.docker.com/compose/)  
- An existing external Docker network named `docker-hadoop_default` (for Hadoop integration)  

To create the network (if not already available):

```bash
docker network create docker-hadoop_default
```

## 📂 Folder Structure
```bash
spark_docker/
├── docker-compose.yml
├── jupyter/
│   ├── Dockerfile
│   └── volume/       # Mounted workspace for notebooks
├── data/             # Shared data between Jupyter and Spark
└── ...
```

## ⚡ Usage

### 1. Clone the Repository

```bash
git clone https://github.com/hoanghaithanh/spark_docker.git
cd spark_docker
```

### 2. Set Jupyter Token  
Update your `.env` file or export a token before starting:

```bash
export JUPYTER_TOKEN=your_secure_token
```

### 3. Start the Services

```bash
docker-compose up -d
```

### 4. Access the Services
- Jupyter Notebook: http://localhost:8888  
- Spark Master Web UI: http://localhost:9090

## 📊 Volumes

- `./jupyter/volume` → `/home/jovyan/work` (Jupyter workspace)  
- `./data` → `/home/jovyan/data` (Shared data)  
- `/etc/letsencrypt` → `/etc/letsencrypt` (SSL certificates if available)  

## 🔧 Stopping the Services
```bash
docker-compose down
```


## 📜 License

This project is licensed under the MIT License – feel free to use and modify.

---

💡 Tip: You can extend this setup with additional Spark workers by scaling the `spark-worker` service:
```bash
docker-compose up -d --scale spark-worker=3
```
