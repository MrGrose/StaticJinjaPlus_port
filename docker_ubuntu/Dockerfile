FROM ubuntu:24.04

RUN apt-get update && apt-get install -y --no-install-recommends \
    python3.12 \
    python3-pip \ 
    python3-venv \
    && rm -rf /var/lib/apt/lists/*

ENV VIRTUAL_ENV=/project/venv
WORKDIR /project
ARG VERSION=0.1.1
ARG HASH=30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b
ADD --checksum=sha256:${HASH}\
    https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${VERSION}.tar.gz SJP.tar.gz
RUN tar xzf SJP.tar.gz --strip-components=1 && rm SJP.tar.gz

RUN python3.12 -m venv $VIRTUAL_ENV \
    && . venv/bin/activate \
    && pip install -r requirements.txt 

ENV PATH="$VIRTUAL_ENV/bin:$PATH"

CMD ["python3", "main.py", "--srcpath", "/project/templates", "--outpath", "/project/build"]