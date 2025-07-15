## StaticJinjaPlus Docker Port
Порт для сборки Docker-образов [StaticJinjaPlus](https://github.com/MrDave/StaticJinjaPlus) из исходников оригинального репозитория.

### О проекте
Порт — это набор Dockerfile'ов и инструкций, которые позволяют:

- Скачать исходники StaticJinjaPlus из официального репозитория по нужной версии или из ветки разработки.

- Собрать [Docker-образ](https://www.docker.com/get-started/) на выбранной базе (Ubuntu или Python Slim).

- Запустить контейнер.


## Как собрать Docker-образ

1. Сборка версии (Python Slim):
```bash
docker build -f docker_slim/Dockerfile -t static-jinja-plus:0.1.1-slim 
docker build -f docker_slim_dev/Dockerfile -t static-jinja-plus:develop-slim 
```
При создании образа 0.1.0 надо явно указать хэш и версию
```bash
docker build -f docker_slim/Dockerfile -t static-jinja-plus:0.1.0-slim \
    --build-arg VERSION=0.1.0 \
    --build-arg HASH=3555bcfd670e134e8360ad934cb5bad1bbe2a7dad24ba7cafa0a3bb8b23c6444
```

2. Сборка версии на базе Ubuntu:

```bash
docker build -f docker_ubuntu/Dockerfile -t static-jinja-plus:0.1.1-ubuntu
docker build -f docker_ubuntu_dev/Dockerfile -t static-jinja-plus:develop-ubuntu
```

При создании образа 0.1.0 надо явно указать хэш и версию
```bash
docker build -f docker_ubuntu/Dockerfile -t static-jinja-plus:0.1.1-ubuntu \
    --build-arg VERSION=0.1.0 \
    --build-arg HASH=3555bcfd670e134e8360ad934cb5bad1bbe2a7dad24ba7cafa0a3bb8b23c6444
```

## Как это работает

- Dockerfile скачивает архив исходников StaticJinjaPlus с GitHub по нужной версии (тегу) или из ветки main.
- Для разных базовых образов используются разные Dockerfile: slim — для минимального размера, ubuntu — для расширенной среды.
- Образы запушены на [Dockerhub](https://hub.docker.com/r/grroma/static-jinja-plus).

## Цель проекта
Код написан в образовательных целях на онлайн-курсе [dvmn.org](https://dvmn.org/modules/).