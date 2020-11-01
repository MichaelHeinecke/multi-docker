FROM node:alpine AS builder
WORKDIR /app
COPY package.json .
RUN npm config set registry http://registry.npmjs.org/
RUN npm install
COPY . .
RUN npm run build

FROM nginx
# port for incoming traffic on AWS elastic beanstalk
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
# only copy contents of build directory
COPY --from=builder /app/build /usr/share/nginx/html
