FROM ubuntu:22.04

ARG STATICJINJAPLUS_VERSION=latest
ENV STATICJINJAPLUS_VERSION=${STATICJINJAPLUS_VERSION}

WORKDIR /opt/StaticJinjaPlus

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        curl \
        ca-certificates \
        python3 \
        python3-pip \
        python3-venv && \
    rm -rf /var/lib/apt/lists/*

RUN if [ "$STATICJINJAPLUS_VERSION" = "main" ]; then \
      curl -L https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.tar.gz -o /tmp/app.tar.gz ; \
    else \
      curl -L https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${STATICJINJAPLUS_VERSION}.tar.gz -o /tmp/app.tar.gz ; \
    fi

RUN tar -xzf /tmp/app.tar.gz --strip-components=1 -C /opt/StaticJinjaPlus && rm /tmp/app.tar.gz

RUN python3 -m venv /opt/venv

ENV PATH="/opt/venv/bin:$PATH"

RUN pip install --no-cache-dir -r requirements.txt