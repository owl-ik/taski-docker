FROM node:18 AS build

WORKDIR /app

# Копируем только файлы, необходимые для установки зависимостей
COPY package.json package-lock.json ./

# Устанавливаем зависимости
RUN npm install

# Копируем остальные файлы проекта
COPY . .

# Собираем проект
RUN npm run build

# Финальный образ
FROM node:18-alpine

WORKDIR /app

# Копируем только собранные файлы из стадии build
COPY --from=build /app/build ./build

# Устанавливаем http-server для раздачи статики
RUN npm install -g http-server

# Открываем порт и запускаем сервер
EXPOSE 8000
CMD ["http-server", "build", "-p", "8000"]