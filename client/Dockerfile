# Build Phase
FROM node:lts-alpine as builder

WORKDIR '/app'

COPY package.json .
RUN npm install

COPY . .
RUN npm run build

# Run Phase
FROM nginx
EXPOSE 3000

# override default config with the local custom config
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# nginx will automatically run the server after copying the files
COPY --from=builder /app/build /usr/share/nginx/html 
