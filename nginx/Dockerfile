# Build the user-gui module
FROM node:lts-alpine as user-gui
WORKDIR /app
COPY ./olahd_user_frontend/package*.json ./
COPY ./olahd_user_frontend/yarn.lock ./
RUN yarn install
COPY ./olahd_user_frontend/. .
RUN yarn build

# Build the admin-gui module
FROM node:lts-alpine as admin-gui
WORKDIR /app
COPY ./olahd_admin_frontend/package*.json ./
COPY ./olahd_admin_frontend/yarn.lock ./
RUN yarn install
COPY ./olahd_admin_frontend/. .
RUN yarn build

# Production stage
FROM nginx:stable-alpine
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx/nginx.conf /etc/nginx
COPY ./nginx/conf /etc/nginx/conf.d

# For user-gui
COPY --from=user-gui /app/dist /usr/share/nginx/html/home

# For admin-gui
COPY --from=admin-gui /app/dist /usr/share/nginx/html/admin

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
