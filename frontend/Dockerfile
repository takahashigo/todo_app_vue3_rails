FROM node:16.17.1-bullseye
ARG WORKDIR

ENV HOME=/${WORKDIR}

WORKDIR ${HOME}

RUN apt update \
    && yarn install

#=== 以下を追加
COPY . ./
COPY package.json /app/package.json
COPY yarn.lock /app/yarn.lock

EXPOSE 5173
#=== 以下を追加
CMD ["yarn", "dev", "--host"]
