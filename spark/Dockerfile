FROM bellsoft/liberica-openjdk-alpine:8u282

RUN apk --update add wget tar bash coreutils procps openssl

RUN addgroup -S -g 1000 spark-users \
        && adduser --disabled-password --uid 1001 spark-user spark-users

RUN mkdir /spark-app

WORKDIR /spark-app

COPY . /spark-app

RUN chown -R spark-user:spark-users /spark-app

USER spark-user

ENV SPARK_VERSION=2.4.5
ENV HADOOP_VERSION=2.7
ENV SPARK_HOME=/spark-app/spark
ENV PATH=${SPARK_HOME}/bin:$PATH

RUN mkdir temp && cd temp && \
            wget https://archive.apache.org/dist/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
            tar -xf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && \
            mkdir ${SPARK_HOME} && \
            mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}/* ${SPARK_HOME} && \
            cd / && \
            rm -rf temp