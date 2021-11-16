ARG ELK_VERSION

FROM ubuntu as builder

ADD https://github.com/coccoc/coccoc-tokenizer/archive/refs/heads/master.zip /
RUN apt-get update -y && apt-get install -y unzip cmake g++ default-jdk

RUN unzip master.zip && chmod 755 coccoc-tokenizer-master && \
    cd coccoc-tokenizer-master && mkdir build && cd build && \
    cmake -DBUILD_JAVA=1 -DCMAKE_INSTALL_PREFIX=/usr .. && \
    make install && \
    cp libcoccoc_tokenizer_jni.so /usr/lib/ && \
    cd / && rm -f master.zip && \
    rm -rf coccoc-tokenizer-master

# https://www.docker.elastic.co/
FROM docker.elastic.co/elasticsearch/elasticsearch:${ELK_VERSION}
COPY --from=builder /usr/lib/ /usr/lib/
# make an additional directory for cococ tokenizer dicts
RUN mkdir -p /usr/local/share/tokenizer/dicts
COPY dicts/* /usr/local/share/tokenizer/dicts
# Add elasticsearch plugins setup
ARG ELK_VERSION
COPY elasticsearch-analysis-vietnamese-${ELK_VERSION}.zip /usr/share/elasticsearch
RUN bin/elasticsearch-plugin install --batch file:///usr/share/elasticsearch/elasticsearch-analysis-vietnamese-${ELK_VERSION}.zip
RUN bin/elasticsearch-plugin install analysis-icu
