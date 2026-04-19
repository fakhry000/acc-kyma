ARG BASE_IMAGE=docker.n8n.io/n8nio/runners:2.15.0
FROM ${BASE_IMAGE}
USER root
RUN python -m pip install --no-cache-dir --upgrade pip
COPY requirements.txt /tmp/requirements.txt
RUN python -m pip install --no-cache-dir -r /tmp/requirements.txt && rm -f /tmp/requirements.txt
USER 65532:65532
