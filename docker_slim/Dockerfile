FROM python:3.12-slim

WORKDIR /project
ARG VERSION=0.1.1
ARG HASH=30d9424df1eddb73912b0e2ad5375fa2c876c8e30906bec91952dfb75dcf220b
ADD --checksum=sha256:${HASH}\
    https://github.com/MrDave/StaticJinjaPlus/archive/refs/tags/${VERSION}.tar.gz SJP.tar.gz
RUN tar xzf SJP.tar.gz --strip-components=1 && rm SJP.tar.gz

RUN  pip install -r requirements.txt 

CMD ["python", "main.py", "--srcpath", "/project/templates", "--outpath", "/project/build"]