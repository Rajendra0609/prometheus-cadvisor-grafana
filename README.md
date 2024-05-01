# prometheus-cadvisor-grafana



firewall-cmd --zone=public --add-port=9323/tcp
Open /etc/docker/daemon.json and add the following.

{
  "metrics-addr" : "0.0.0.0:9323",
  "experimental" : true
}


Update `prometheus.yml`.

Edit the prometheus.yml file in the /root directory.

vi ~/prometheus.yml
Change the contents to reflect the following:

scrape_configs:
  - job_name: prometheus
    scrape_interval: 5s
    static_configs:
    - targets:
      - prometheus:9090
      - node-exporter:9100
      - pushgateway:9091
      - cadvisor:8080

  - job_name: docker
    scrape_interval: 5s
    static_configs:
    - targets:
      - PRIVATE_IP_ADDRESS:9323



docker-compose up
