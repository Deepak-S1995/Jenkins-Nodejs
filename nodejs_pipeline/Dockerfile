FROM node:16.17.0 AS builder
# Environment

WORKDIR /app
#ENV NODE_ENV=production

# Dependencies

COPY package.json /app/
COPY tailwind.config.js /app/
COPY tsconfig.json /app/

#COPY packages/addon/package.json /app/packages/addon/
#COPY packages/addon/yarn.lock /app/packages/addon/

COPY ./src /app/src
COPY ./public /app/public

RUN npm install 
#RUN npx lerna bootstrap 

# Build

COPY . /app/
#COPY packages/skyplus-design-system-app/dist packages/login/node_modules/skyplus-design-system-app/dist
RUN npm run build
RUN ls
RUN pwd
#RUN cd packages/addon && yarn build
#RUN ls
#RUN pwd

# Serve

FROM nginxinc/nginx-unprivileged 
COPY --from=builder /app/build /usr/share/nginx/html