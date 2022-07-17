FROM node:14-alpine
RUN apk --no-cache add python3 make gcc g++ fontconfig ttf-dejavu curl 
WORKDIR /app
COPY . .
RUN npm install
ENTRYPOINT ["node", "index.js"]
EXPOSE 3005:3005