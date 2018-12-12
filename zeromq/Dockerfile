FROM buildpack-deps:14.04 as builder

MAINTAINER Galaxyobe Automated Build Project <galaxyobe@qq.com>

RUN cd /tmp && wget https://github.com/zeromq/libzmq/releases/download/v4.2.5/zeromq-4.2.5.tar.gz
RUN cd /tmp && tar xf zeromq-4.2.5.tar.gz && cd zeromq-4.2.5 && ./configure && make -j 4 && chmod 644 src/libzmq.la



FROM alpine

MAINTAINER Galaxyobe Automated Build Project <galaxyobe@qq.com>

COPY --from=builder /tmp/zeromq-4.2.5/src/libzmq.la /usr/local/lib
COPY --from=builder /tmp/zeromq-4.2.5/src/.libs/libzmq.so.5.1.5 /usr/local/lib/libzmq.so.5.1.5
COPY --from=builder /tmp/zeromq-4.2.5/src/.libs/libzmq.lai /usr/local/lib/libzmq.la
COPY --from=builder /tmp/zeromq-4.2.5/src/.libs/libzmq.a /usr/local/lib/libzmq.a

RUN cd /usr/local/lib && { ln -s -f libzmq.so.5.1.5 libzmq.so.5 || { rm -f libzmq.so.5 && ln -s libzmq.so.5.1.5 libzmq.so.5; }; }
RUN cd /usr/local/lib && { ln -s -f libzmq.so.5.1.5 libzmq.so || { rm -f libzmq.so && ln -s libzmq.so.5.1.5 libzmq.so; }; }


RUN ldconfig -n /usr/local/lib
