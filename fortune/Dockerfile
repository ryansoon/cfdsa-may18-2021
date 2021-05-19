# the base image
FROM node:16

# define some env variables
ENV APP_ROOT=/app APP_PORT=3000

## build the image
# create the /app dir and cd into /app
WORKDIR ${APP_ROOT}

# inside APP_ROOT
# copy the following files
ADD main.js .
ADD package.json .
ADD package-lock.json .
# copy these directories
ADD public public
ADD views views

# install the packages in package.json 
RUN npm install

## running the image
# add healthcheck
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/healthz || exit 1

# document that this container listens on port 3000
EXPOSE ${APP_PORT}

# run the application
ENTRYPOINT [ "node", "main.js" ]
