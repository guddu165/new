# my global config
global:
  scrape_interval: 15s # Set the scrape interval to every 15 seconds. Default is every 1 minute.
  evaluation_interval: 15s # Evaluate rules every 15 seconds. The default is every 1 minute.
  # scrape_timeout is set to the global default (10s).

# Alertmanager configuration
alerting:
  alertmanagers:
    - static_configs:
        - targets:
           - 0.0.0.0:9093

# Load rules once and periodically evaluate them according to the global 'evaluation_interval'.
rule_files:
  - "prometheus_rules.yml"
  # - "first_rules.yml"
  # - "second_rules.yml"

# A scrape configuration containing exactly one endpoint to scrape:
# Here it's Prometheus itself.
scrape_configs:
  # The job name is added as a label `job=<job_name>` to any timeseries scraped from this config.
  - job_name: "prometheus"

    # metrics_path defaults to '/metrics'
    # scheme defaults to 'http'.

    static_configs:
      - targets: ["0.0.0.0:9090"]

  - job_name: "node_exporter"
    static_configs:
      - targets: ["0.0.0.0:9100"]

  - job_name: "mysqld_exporter"
    metrics_path: /metrics
    scheme: http
    static_configs:
      - targets: ["0.0.0.0:9104"]
