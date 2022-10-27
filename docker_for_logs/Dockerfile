FROM golang:latest

ENV ARCHITECTURE=linux-arm64
RUN go install github.com/mingrammer/flog@latest

RUN apt-get update

RUN apt-get install -y wget \
                       vim \
                       unzip

WORKDIR /root
RUN wget https://github.com/grafana/loki/releases/download/v2.5.0/promtail-${ARCHITECTURE}.zip \
    && unzip promtail-${ARCHITECTURE}.zip \
    && rm promtail-${ARCHITECTURE}.zip

COPY promtail-local-config.yaml .

ENTRYPOINT ["/go/bin/flog"]

CMD ["-l", "-d", "30ms", "-o", "/root/logs/apache.log", "-t", "log"]