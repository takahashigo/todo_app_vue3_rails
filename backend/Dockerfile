#=== 軽量slim系イメージを使用。
FROM ruby:3.1.2-bullseye
#=== docker-compose.ymlから渡されたもの
ARG WORKDIR
#=== インストールするパッケージ
ARG RUNTIME_PACKAGES="build-essential tzdata git less"

ENV HOME=/${WORKDIR}

WORKDIR ${HOME}

RUN apt-get update \
    && apt-get install -y --no-install-recommends ${RUNTIME_PACKAGES} \
    && apt-get clean \
    && rm -rf /var/cache/apt/archives/* \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

COPY Gemfile /app/Gemfile
COPY Gemfile.lock /app/Gemfile.lock

ENV LANG=C.UTF-8 \
    TZ=Asia/Tokyo

#=== Bundlerを最新のものに
RUN gem update --system \
    && gem install bundler
RUN bundle install

COPY . ./
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
