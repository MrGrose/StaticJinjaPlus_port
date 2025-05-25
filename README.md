## StaticJinjaPlus Docker Port
Порт для сборки Docker-образов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) из исходников оригинального репозитория.

### О проекте
Порт — это набор Dockerfile'ов и инструкций, которые позволяют:

- Скачать исходники StaticJinjaPlus из официального репозитория по нужной версии или из ветки разработки.

- Собрать [Docker-образ](https://www.docker.com/get-started/) на выбранной базе (Ubuntu или Python Slim).

- Запустить контейнер.


### Структура
- `Dockerfile.slim` — универсальный Dockerfile для Python Slim, поддерживает параметризацию версии через ARG.
- `Dockerfile.ubuntu` — универсальный Dockerfile для Ubuntu, поддерживает параметризацию версии через ARG.

## Как собрать Docker-образ

1. Сборка образа с нужной версией (Python Slim)

```bash
docker build -f Dockerfile.slim
--build-arg STATICJINJAPLUS_VERSION=0.1.1
-t you_name/staticjinjaplus:0.1.1-slim .
```

2. Сборка develop-образа (из main-ветки, Python Slim)

```bash
docker build -f Dockerfile.slim
--build-arg STATICJINJAPLUS_VERSION=main
-t you_name/staticjinjaplus:develop-slim .
```

3. Сборка образа на базе Ubuntu

```bash
docker build -f Dockerfile.ubuntu
--build-arg STATICJINJAPLUS_VERSION=0.1.1
-t you_name/staticjinjaplus:0.1.1-ubuntu .
```

4. Сборка develop-образа (из main-ветки, Ubuntu)


```bash
docker build -f Dockerfile.ubuntu
--build-arg STATICJINJAPLUS_VERSION=main
-t you_name/staticjinjaplus:develop-ubuntu .
```

5. Посмотреть образы
```bash
docker images
```

6. Пример запуска контейнера

```bash
docker run --rm -it you_name/staticjinjaplus:0.1.1-slim
```


## Пример команд для сборки

| Базовый образ      | Версия StaticJinjaPlus | Dockerfile         | Пример команды                                                                 |
|--------------------|-----------------------|--------------------|--------------------------------------------------------------------------------|
| python:3.12-slim   | 0.1.1                 | Dockerfile.slim    | `docker build -f Dockerfile.slim --build-arg STATICJINJAPLUS_VERSION=0.1.1 -t you_name/staticjinjaplus:0.1.1-slim .` |
| ubuntu:22.04       | 0.1.1                 | Dockerfile.ubuntu  | `docker build -f Dockerfile.ubuntu --build-arg STATICJINJAPLUS_VERSION=0.1.1 -t you_name/staticjinjaplus:0.1.1-ubuntu .` |
| python:3.12-slim   | main (develop)        | Dockerfile.slim    | `docker build -f Dockerfile.slim --build-arg STATICJINJAPLUS_VERSION=main -t you_name/staticjinjaplus:develop-slim .` |
| ubuntu:22.04       | main (develop)        | Dockerfile.ubuntu  | `docker build -f Dockerfile.ubuntu --build-arg STATICJINJAPLUS_VERSION=main -t you_name/staticjinjaplus:develop-ubuntu .` |

---

## Как это работает

- Dockerfile скачивает архив исходников StaticJinjaPlus с GitHub по нужной версии (тегу) или из ветки main.
- Сборка параметризуется через `ARG STATICJINJAPLUS_VERSION`.
- Для разных базовых образов используются разные Dockerfile: slim — для минимального размера, ubuntu — для расширенной среды.
