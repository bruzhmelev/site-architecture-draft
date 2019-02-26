# README

## Схема развертывания

### Верхнеуровневая схема

https://drive.google.com/file/d/1lpRfKpWtapd6qBiqrR3VwFxw9XJ1Vl0K/view?usp=sharing
![Верхнеуровневая схема](https://i.imgur.com/jscnK6s.png)

### Схема развертывания по серверам

Вырезать из общей схемы(ниже) или дорисовать

### Детальная схема для сайта (учитывая все NGINX, Prometheus, Kibana, Zipkin, CDN)

[Нарисовать]

### Общая схема архитектуры DodoIS для представления роли во всей системе

https://drive.google.com/file/d/1fT34iQl9mfiJ2IQ4IzExZYA4epWn7fYL/view
![Сервера](https://i.imgur.com/7S6ONxp.png)

https://drive.google.com/file/d/1CIiX8XfHv49w2q9Fl3q3FzPcw8Q4FlYc/view
![Архитектура DodoIS](https://i.imgur.com/Mf7EahA.png)

### Схема как создаётся заказ

## Deploy

### Как сбилдить

### Как задеплоить dev/prod. Нейминг окружений

## Внутренее устройство Backend компонент

### Общая схема взаимодействия компонент

### Описание каждой компоненты в двух предложениях. Зона ответственности. Взаимодействие с другими компонентами

1. Controllers - только обработка сетевых запросов и передача управления в AppServices.
   1. SiteController - отдаёт html.
   2. Остальные контроллеры - api, отдающее json.
2. AppServices - логика сценариев.
3. Workflow - стейтмашина, управление состоянием корзины клиента, не должна содержать логики приложения, не ходит в DataServices. .
4. DataServices - все походы во внешние сервисы (Upsell, LegacyFacade, PaymentGateway)
5. Repositories - репозитории, чтение/запись в свои Persist.
   1. Пример, RedisWorkflowStore - репозиторий хранящий стейт клиента(корзину)
6. ModelBuilder, ModelTransformers - создают вьюмодели
   1. Transformers - мапперы.
   2. Builder - ещё ходят в DataServices.
7. Resources - файлы переводов.
8. Cachign - реализации кеша/CacheManager. SuperCache/InMemoryCache.
9. Domain - не то что вы могли бы подумать, т.к. вся основная логика приложения сосредоточена в AppServices, поэтому здесь в основном всё что не поместилось в остальные проекты
   1. Services - что-то, что почему-то не попадает в AppServices.
   2. Workflow и всё что с ним связанно.
   3. Интерфейсы(датасервисов, репозиториев), для общего использования.
   4. Model - 

## Структура Frontend

1. Папка `./Client`, плюс файлы конфигурации на этом же уровне - весь фронтенд.
2. `EntryPoint` (Desktop/Mobile) - входные точки для инициалицации фронтенда, первоначального рендера.

### Верхнеуровнево взаимодействие с Backend, CDN и т.п. Подробно архитектура будет описанна в отдельном документе
