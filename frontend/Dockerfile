FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# To run the built application, you might want to use a web server like nginx.
# Here's an example of how to serve the built files using nginx:
FROM nginx:alpine
RUN rm -rf /usr/share/nginx/html/*
RUN mkdir -p /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
