FROM alpine AS build

# Environment Variables
ENV REACT_APP_BACKEND_WS=ws://localhost:8080
ENV REACT_APP_BACKEND_URL=http://localhost:8080

RUN apk add --no-cache nodejs-current npm 

ADD . /app/frontend
WORKDIR /app/frontend

# Depedencies
RUN npm install

# DEV STAGE IMAGE
FROM build AS dev
COPY . .
RUN npm install
CMD npm start

# PRD STAGE IMAGE
FROM build AS Release
COPY . .
RUN npm run build
CMD npm start

