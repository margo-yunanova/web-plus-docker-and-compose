# С помощью директивы AS можно дать образу имя
FROM node:19.7-alpine AS builder

WORKDIR /app

COPY package*.json ./

# Устанавливаем зависимости
RUN npm ci

# Копируем исходный код и собираем приложение
COPY . ./

RUN npm run build


FROM nginx as production


COPY nginx/conf.d/default.conf /etc/nginx/conf.d/

# С помощью параметера --from указываем, что копировать нужно из образа builder
# Копируем директорию со сборкой приложения
COPY --from=builder /app/build/* /usr/share/nginx/html/
