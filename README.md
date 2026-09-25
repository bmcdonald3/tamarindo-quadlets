# Deploying with this repo

mkdir -p /etc/containers/systemd
mkdir -p /data/oci
mkdir -p /data/boot-images
mkdir -p /data/postgres
mkdir -p /etc/openchami

Create /etc/containers/systemd/openchami.network

Create /etc/containers/systemd/postgres.container

Create /etc/containers/systemd/smd.container

Create /etc/containers/systemd/smd-init.container

Create /etc/containers/systemd/coredhcp.container

Create /etc/containers/systemd/boot-service.container

Create /etc/containers/systemd/registry.container

Create /etc/containers/systemd/openchami-haproxy.container

Create a HAProxy config at /etc/openchami/haproxy.cfg

curl -LO $(curl -s https://api.github.com/repos/openchami/versitygw-quadlet/releases/latest | grep "browser_download_url.*\.rpm" | grep -v "\.src\.rpm" | cut -d '"' -f 4) zypper in -y ./versitygw-quadlet-*.noarch.rpm
zypper in -y https://github.com/openchami/versitygw-quadlet/releases/latest/download/versitygw-quadlet.x86_64.rpm


systemctl daemon-reload

systemctl enable --now versitygw-gensecrets.service
systemctl enable --now versitygw.service

systemctl start openchami-network.service
systemctl start postgres.service
systemctl start smd.service
systemctl start coredhcp.service
systemctl start boot-service.service
systemctl start registry.service
systemctl start openchami-haproxy.service
