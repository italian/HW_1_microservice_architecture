# Микросервисная архитектура для прогнозирования диабета

Проект представляет собой микросервисное приложение для прогнозирования диабета на основе различных медицинских показателей. Система состоит из нескольких взаимодействующих через RabbitMQ сервисов и обеспечивает непрерывный процесс предсказания и оценки точности модели.

## Структура проекта

```
microservice_architecture/
├── docker-compose.yml        # Конфигурация Docker Compose
├── features/                 # Сервис генерации признаков
│   ├── Dockerfile
│   ├── requirements.txt
│   └── src/
│       └── features.py
├── model/                    # Сервис с моделью
│   ├── Dockerfile
│   ├── requirements.txt
│   ├── myfile.pkl           # Сериализованная модель
│   └── src/
│       └── model.py
├── metric/                   # Сервис расчета метрик
│   ├── Dockerfile
│   ├── requirements.txt
│   └── src/
│       └── metric.py
├── plot/                     # Сервис визуализации
│   ├── Dockerfile
│   ├── requirements.txt
│   └── plot.py
└── logs/                     # Директория для логов
```

## Описание сервисов

1. **Features Service**: Генерирует векторы признаков из датасета о диабете и отправляет их в очередь.
2. **Model Service**: Получает векторы признаков, делает предсказания и отправляет их в очередь.
3. **Metric Service**: Рассчитывает абсолютную ошибку между предсказаниями и реальными значениями.
4. **Plot Service**: Создает и обновляет визуализацию распределения ошибок.

## Инструкция по запуску

1. Убедитесь, что у вас установлен Docker и Docker Compose

2. Клонируйте репозиторий:
```bash
git clone git@github.com:italian/HW_1_microservice_architecture.git
cd microservice_architecture
```

3. Запустите приложение:
```bash
docker-compose up --build
```

4. Для остановки приложения используйте:
```bash
docker-compose down
```

## Мониторинг работы

- RabbitMQ интерфейс доступен по адресу: http://localhost:15672 (guest/guest)
- Метрики сохраняются в файл: logs/metric_log.csv
- График распределения ошибок: logs/error_distribution.png

## Используемые технологии

- Python 3.9
- RabbitMQ
- Docker & Docker Compose
- scikit-learn
- pandas
- matplotlib
- pika (AMQP client)
