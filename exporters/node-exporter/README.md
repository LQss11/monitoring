# Node exporter
## Install
### Host
Run the following commands:
```sh
# NOTE: Replace the URL with one from the above mentioned "downloads" page.
# <VERSION>, <OS>, and <ARCH> are placeholders.
wget https://github.com/prometheus/node_exporter/releases/download/v<VERSION>/node_exporter-<VERSION>.<OS>-<ARCH>.tar.gz
tar xvfz node_exporter-*.*-amd64.tar.gz
cd node_exporter-*.*-amd64
./node_exporter
```

# References
- [Monitoring Linux host metrics with the Node Exporter](https://prometheus.io/docs/guides/node-exporter/)