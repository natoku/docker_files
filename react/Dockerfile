#FROM node:13.12.0-alpine
#FROM node:14-alpine
#
#WORKDIR /app
#
#COPY . .
##ENV PATH /app/node_modules/.bin:$PATH
#
##COPY package.json ./
##COPY package-lock.json ./
#RUN npm install
##RUN npm install react-scripts@3.4.1 -g --silent
#CMD ["npm", "start"]
#EXPOSE 3000
# pull the official base image

##FROM node:14-alpine
### set working direction
##WORKDIR /app
### add `/app/node_modules/.bin` to $PATH
##ENV PATH /app/node_modules/.bin:$PATH
### install application dependencies
##COPY package.json ./
##COPY package-lock.json ./
##RUN npm i
### add app
##RUN npm run build
##COPY ./build ./
### start app
##CMD ["npm", "start"]


## Stage 1 - the build process
#FROM node:12.16.2 as build-deps
#WORKDIR /usr/src/app
#COPY package.json ./
#RUN npm i
#COPY . .
#RUN npm run build
#
## Stage 2 - the production environment
#FROM nginx:1.17-alpine
#COPY --from=build-deps /usr/src/app/build /usr/share/nginx/html
#RUN rm /etc/nginx/conf.d/default.conf
#COPY nginx/nginx.conf /etc/nginx/conf.d
#EXPOSE 80
#CMD ["nginx", "-g", "daemon off;"]



# Stage 0, "build-stage", based on Node.js, to build and compile the frontend
#FROM tiangolo/node-frontend:10 as build-stage
#WORKDIR /app
#COPY package*.json /app/
#RUN npm install
#COPY ./ /app
#RUN npm run build
## Stage 1, based on Nginx, to have only the compiled app, ready for production with Nginx
#FROM nginx:1.15
#COPY --from=build-stage /app/build/ /usr/share/nginx/html
## Copy the default nginx.conf provided by tiangolo/node-frontend
#COPY --from=build-stage /nginx.conf /etc/nginx/conf.d/default.conf


FROM node:14 AS builder
# Set working directory
WORKDIR /app
# Copy all files from current directory to working dir in image
COPY . .
# install node modules and build assets
RUN yarn install && yarn build

# nginx state for serving content
FROM nginx:alpine
# Set working directory to nginx asset directory
WORKDIR /usr/share/nginx/html
# Remove default nginx static assets
RUN rm -rf ./*
# Copy static assets from builder stage
COPY --from=builder /app/build .
# Containers run nginx with global directives and daemon off
ENTRYPOINT ["nginx", "-g", "daemon off;"]