FROM python:3.12-slim

WORKDIR /project
ADD  https://github.com/MrDave/StaticJinjaPlus/archive/refs/heads/main.tar.gz SJP.tar.gz
RUN tar xzf SJP.tar.gz --strip-components=1 && rm SJP.tar.gz

RUN  pip install -r requirements.txt 

CMD ["python", "main.py", "--srcpath", "/project/templates", "--outpath", "/project/build"]