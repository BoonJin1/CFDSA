# base imge - ':' refers to tag
# if using a basic app (e.g. ubuntu), need to install e.g. node/python
FROM node:latest

# define env variables - can be used within the main script
ENV APP_PORT=3000
ENV APP_ROOT=/app
# ENV APP_PORT=3000 APP_ROOT=/app

# create APP_ROOT dir and cd inside
WORKDIR ${APP_ROOT}

# copy all required files into APP_ROOT
# ADD <file> <copy to path>
# ADD will recursively copy folders and subfolders
# ADD can also apply to remote addr (e.g. https://...)
# ADD is different from COPY
ADD main.js .
ADD package-lock.json .
ADD package.json .
ADD public public
ADD views views

# install dependencies
# reads from package.json
# for python - RUN pip install -r requirements.txt
# typical linux command, can stack -> RUN npm install && echo "all done"
RUN npm install

# as of this point all lines above are for building the image
# lines below are for execution

# configure health checks -> checks status
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD curl -s -f http://localhost:${APP_PORT}/health > /dev/null || exit 1

# specify port number
# by default uses tcp (no need specify)
EXPOSE ${APP_PORT}

# how to run the program
# cannot call RUN here -> will assume as part of the build 
ENTRYPOINT [ "node", "main.js" ]
# CMD [ "3000" ]
# ^ hardcoded port number