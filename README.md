## StaticJinjaPlus Docker Port
Порт для сборки Docker-образов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) из исходников оригинального репозитория.

### О проекте
Порт — это набор Dockerfile'ов и инструкций, которые позволяют:

- Скачать исходники StaticJinjaPlus из официального репозитория по нужной версии или из ветки разработки.

- Собрать [Docker-образ](https://www.docker.com/get-started/) на выбранной базе (Ubuntu или Python Slim).

- Запустить контейнер.


### Структура
- `docker_slim/Dockerfile` — универсальный Dockerfile для Python Slim, поддерживает параметризацию версии через ARG.
- `docker_ubuntu/Dockerfile` — универсальный Dockerfile для Ubuntu, поддерживает параметризацию версии через ARG.


## Как собрать Docker-образ
Чтобы собрать образ с нужной версией StaticJinjaPlus, укажите тег в аргументе `STATICJINJAPLUS_VERSION`.

1. Сборка стабильной версии (Python Slim):

```bash
docker build -f docker_slim/Dockerfile --build-arg STATICJINJAPLUS_VERSION=0.1.1 -t static-jinja-plus:0.1.1-slim .
docker build -f docker_slim/Dockerfile --build-arg STATICJINJAPLUS_VERSION=0.1.0 -t static-jinja-plus:0.1.0-slim .
docker build -f docker_slim/Dockerfile --build-arg STATICJINJAPLUS_VERSION=main -t static-jinja-plus:develop-slim .
```

2. Сборка стабильной версии на базе Ubuntu:

```bash
docker build -f docker_ubuntu/Dockerfile --build-arg STATICJINJAPLUS_VERSION=0.1.1 -t static-jinja-plus:0.1.1-ubuntu .
docker build -f docker_ubuntu/Dockerfile --build-arg STATICJINJAPLUS_VERSION=0.1.0 -t static-jinja-plus:0.1.0-ubuntu .
docker build -f docker_ubuntu/Dockerfile --build-arg STATICJINJAPLUS_VERSION=main -t static-jinja-plus:develop-ubuntu .
```


## Как запустить контейнер
Рекомендованная стабильная версия. 
Пример запуска контейнера:
```bash
docker run --rm -it static-jinja-plus:0.1.1-slim
docker run --rm -it static-jinja-plus:0.1.0-slim
docker run --rm -it static-jinja-plus:develop-slim
docker run --rm -it static-jinja-plus:0.1.1-ubuntu
docker run --rm -it static-jinja-plus:0.1.0-ubuntu
docker run --rm -it static-jinja-plus:develop-ubuntu
```


## Как это работает

- Dockerfile скачивает архив исходников StaticJinjaPlus с GitHub по нужной версии (тегу) или из ветки main.
- Сборка параметризуется через `ARG STATICJINJAPLUS_VERSION`.
- Для разных базовых образов используются разные Dockerfile: slim — для минимального размера, ubuntu — для расширенной среды.

## Цель проекта
Код написан в образовательных целях на онлайн-курсе [dvmn.org](https://dvmn.org/modules/).