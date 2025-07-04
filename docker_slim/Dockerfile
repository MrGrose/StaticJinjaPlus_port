FROM python:3.12-slim

ARG STATICJINJAPLUS_VERSION=latest
ENV STATICJINJAPLUS_VERSION=${STATICJINJAPLUS_VERSION}

WORKDIR /opt/StaticJinjaPlus

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl python3-venv && \
    rm -rf /var/lib/apt/lists/*

RUN set -e; \
    if [ "$STATICJINJAPLUS_VERSION" = "main" ]; then \
        URL="https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.tar.gz"; \
        HASH="9adccb8fe17a40252df1a3acdea7edef4633b4ecaa8ba2dd5e0270f87ae43eab"; \
    elif [ "$STATICJINJAPLUS_VERSION" = "0.1.0" ]; then \
        URL="https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/0.1.0.tar.gz"; \
        HASH="3555bcfd670e134e8360ad934cb5bad1bbe2a7dad24ba7cafa0a3bb8b23c6444"; \
    elif [ "$STATICJINJAPLUS_VERSION" = "0.1.1" ]; then \
        URL="https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/0.1.1.tar.gz"; \
        HASH="30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b"; \
    else \
        echo "Unsupported version: $STATICJINJAPLUS_VERSION" && exit 1; \
    fi; \
    curl -L "$URL" -o /tmp/app.tar.gz; \
    echo "$HASH  /tmp/app.tar.gz" | sha256sum -c -;

RUN tar -xzf /tmp/app.tar.gz --strip-components=1 -C /opt/StaticJinjaPlus && rm /tmp/app.tar.gz

RUN python3 -m venv /opt/venv

RUN /opt/venv/bin/pip install --no-cache-dir -r requirements.txt

CMD ["sh", "-c", "mkdir -p build && /opt/venv/bin/python main.py --srcpath templates_example --outpath build"]