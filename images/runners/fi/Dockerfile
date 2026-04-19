FROM n8nio/runners:latest
USER root
RUN python -m pip install --no-cache-dir --upgrade pip
COPY requirements.txt /tmp/requirements.txt
RUN python -m pip install --no-cache-dir -r /tmp/requirements.txt && rm -f /tmp/requirements.txt
USER 65532:65532
