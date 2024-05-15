# Обзор бэкенда проекта для хакатона True Tech Hack 
# От МТС

## Применяемые технологии:
1. Postgresql
2. NATS
3. Golang

## Уровни: 

1. Postgresql

В данной БД хранятся все необходимые данные: список событий 
и данные пользователей. Сама БД работает в контейнере.
Подробнее о хранении информации можно узнать из файла 
api.md

2. NATS

В данном случае NATS выполняется функцию брокера сообщений, что
позволяет масштабировать сервис, так как все операции
с БД выполняются только через брокера, поэтому при 
необходимости можно добавить достаточное кол-во
копий БД, чтобы убрать зависимость от единственного образа.
NATS также работает в контейнере.

3. HTTP-сервер

HTTP-сервер выполняет основные функции: передача
событий и авторизация пользователей. HTTP-сервер
предусматривает работу с CORS, что позволяет работать с 
браузером настоящего пользователя. HTTP-сервер также работает
в контейнере.

## Переносимость.

В данном случае все три уровня контейнеризированы, что
позволяет развернуть сервер там, где работает 
докер. 

## Масштабируемость.

Как уже было сказано ранее, благодаря брокеру 
сервис возможно масштабировать по кол-ву копий БД, а также
повторять такие операции, как создание пользователей и 
события, для каждой из копий.

## Golang и библиотеки.

Вся серверная часть написана на языке Golang. Для создания
применялись следующие библиотеки:

1. Chi (более удобный роутинг)
2. Slog (для большего удобства и меньшей зависимости от самой библиотеки логгирования)
3. psql драйвер для postgresql

Остальные библиотеки являются стандартными.


