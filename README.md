# TechOrbit Solutions — Ansible & Monitoring Assignment

## Components
- Ansible — Configuration management
- Prometheus — Metrics collection
- Loki + Promtail — Log collection
- Grafana — Dashboards
- node-exporter — Server metrics agent

## How to Run

### 1. Create Test Servers
- docker run -d --name web01 --hostname web01 ubuntu:22.04 sleep infinity
- docker run -d --name web02 --hostname web02 ubuntu:22.04 sleep infinity
- docker run -d --name db01 --hostname db01 ubuntu:22.04 sleep infinity
- docker run -d --name mon01 --hostname mon01 ubuntu:22.04 sleep infinity

### 2. Setup SSH
- for c in web01 web02 db01 mon01; do
- docker exec $c bash -c "apt update && apt install -y openssh-server python3"
- docker exec $c bash -c "mkdir -p /run/sshd && echo 'root:password' | chpasswd && sed -i 's/#PermitRootLogin.*/PermitRootLogin yes/' /etc/ssh/sshd_config && /usr/sbin/sshd"
done

### 3. Start Monitoring Stack
docker compose up -d

### 4. Verify Ansible
- ansible-inventory --graph
- ansible all -m ping
- ansible-playbook web-setup.yml

### 5. Access Dashboards
- Grafana: http://localhost:3000
- Prometheus: http://localhost:9090/targets

## Author
Sharm | October 2026
