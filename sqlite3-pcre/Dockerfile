# build builder image
FROM alpine AS builder

RUN apk add curl gcc make sqlite-dev pcre-dev musl-dev
RUN mkdir sqlite3-pcre &&\
    curl -fsSL https://github.com/ralight/sqlite3-pcre/archive/refs/heads/master.tar.gz | tar xzv --strip-components=1 --directory=sqlite3-pcre &&\
    cd sqlite3-pcre &&\
    make install

# build final sqlite3-pcre image
FROM alpine 

RUN apk add sqlite pcre

COPY --from=builder /usr/lib/sqlite3/pcre.so /usr/lib/sqlite3/
COPY .sqliterc /root/.sqliterc

VOLUME [ "/data" ]
WORKDIR /data

ENV SQLITE_HISTORY=/data/.sqlite_history

ENTRYPOINT [ "/usr/bin/sqlite3" ]
