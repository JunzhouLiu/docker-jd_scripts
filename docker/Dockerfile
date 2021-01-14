FROM alpine
LABEL AUTHOR="JunzhouLiu <junzhouliu@outlook.com>" \
        VERSION=0.1.2 \
        UPDATE_CONTENT="自用镜像"

RUN set -ex \
        && apk update && apk upgrade\
        && apk add --no-cache tzdata moreutils git nodejs npm curl jq\
        && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
        && echo "Asia/Shanghai" > /etc/timezone

RUN git clone https://gitee.com/lxk0301/jd_scripts.git /scripts \
        && cd /scripts \
        && git checkout master \
        && mkdir logs \
        && npm config set registry https://registry.npm.taobao.org \
        && npm install \
        && cd /tmp \
        && npm install request

ENV BUILD_VERSION=0.1.2 \
        DEFAULT_LIST_FILE=crontab_list.sh \
        CUSTOM_LIST_MERGE_TYPE=append

# github action 构建    
# COPY ./docker/docker_entrypoint.sh /usr/local/bin
# 本地构建
COPY ./docker_entrypoint.sh /usr/local/bin
RUN chmod +x /usr/local/bin/docker_entrypoint.sh

WORKDIR /scripts

ENTRYPOINT ["docker_entrypoint.sh"]
