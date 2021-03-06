# Docker 安装

!!! info "JumpServer 封装了一个 All in one Docker, 可以快速启动。该镜像集成了所需要的组件, 支持使用外置 Database 和 Redis"

## Docker 快速部署

!!! tip ""
    - 使用 root 身份输入
    - 环境迁移和更新升级请检查 SECRET_KEY 是否与之前设置一致, 不能随机生成, 否则数据库所有加密的字段均无法解密

??? tip "Linux 生成随机加密秘钥, 可以用下面的命令"
    ```sh
    if [ ! "$SECRET_KEY" ]; then
      SECRET_KEY=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 50`;
      echo "SECRET_KEY=$SECRET_KEY" >> ~/.bashrc;
      echo $SECRET_KEY;
    else
      echo $SECRET_KEY;
    fi  
    if [ ! "$BOOTSTRAP_TOKEN" ]; then
      BOOTSTRAP_TOKEN=`cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 16`;
      echo "BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN" >> ~/.bashrc;
      echo $BOOTSTRAP_TOKEN;
    else
      echo $BOOTSTRAP_TOKEN;
    fi
    ```

??? tip "macOS 生成随机 key 可以用下面的命令"
    ```sh
    if [ ! "$SECRET_KEY" ]; then
      SECRET_KEY=`LC_CTYPE=C tr -dc A-Za-z0-9 < /dev/urandom | head -c 50`;
      echo "SECRET_KEY=$SECRET_KEY" >> ~/.zshrc;
      echo $SECRET_KEY;
    else
      echo $SECRET_KEY;
    fi  
    if [ ! "$BOOTSTRAP_TOKEN" ]; then
      BOOTSTRAP_TOKEN=`LC_CTYPE=C tr -dc A-Za-z0-9 < /dev/urandom | head -c 16`;
      echo "BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN" >> ~/.zshrc;
      echo $BOOTSTRAP_TOKEN;
    else
      echo $BOOTSTRAP_TOKEN;
    fi
    ```

!!! tip ""
    ```sh
    docker run --name jms_all -d \
      -p 80:80 -p 2222:2222 \
      -e SECRET_KEY=$SECRET_KEY \
      -e BOOTSTRAP_TOKEN=$BOOTSTRAP_TOKEN \
      -v /opt/jumpserver/data:/opt/jumpserver/data \
      -v /opt/jumpserver/mysql:/var/lib/mysql \
      --privileged=true \
      jumpserver/jms_all:v2.3.0
    ```

### 访问

!!! tip ""
    - 浏览器访问: http://<容器所在服务器IP>
    - SSH 访问: ssh -p 2222 <容器所在服务器IP>
    - XShell 等工具请添加 connection 连接, 默认 ssh 端口 2222
    - 默认管理员账户 admin 密码 admin

### 外置数据库要求

!!! tip ""
    - mysql 版本需要大于等于 5.6
    - mariadb 版本需要大于等于 5.5.6
    - 数据库编码要求 uft8

!!! tip "创建数据库"
    ```mysql
    create database jumpserver default charset 'utf8' collate 'utf8_bin';
    grant all on jumpserver.* to 'jumpserver'@'%' identified by 'weakPassword';
    ```


??? info "额外变量说明"
    SECRET_KEY = ******  
    BOOTSTRAP_TOKEN = ******  
    DB_HOST = mysql_host  
    DB_PORT = 3306  
    DB_USER = jumpserver  
    DB_PASSWORD = weakPassword  
    DB_NAME = jumpserver  
    REDIS_HOST = redis_host  
    REDIS_PORT = 6379  
    REDIS_PASSWORD = weakPassword  
    VOLUME /opt/jumpserver/data
    VOLUME /var/lib/mysql


!!! tip ""
    ```sh
    docker run --name jms_all -d \
      -v /opt/jumpserver/data:/opt/jumpserver/data \
      -p 80:80 \
      -p 2222:2222 \
      -e SECRET_KEY=xxxxxx \
      -e BOOTSTRAP_TOKEN=xxx \
      -e DB_HOST=192.168.x.x \
      -e DB_PORT=3306 \
      -e DB_USER=root \
      -e DB_PASSWORD=xxx \
      -e DB_NAME=jumpserver \
      -e REDIS_HOST=192.168.x.x \
      -e REDIS_PORT=6379 \
      -e REDIS_PASSWORD=xxx \
      --privileged=true \
      jumpserver/jms_all:v2.3.0
    ```

## Docker-Compose 部署

!!! info "`.env` 的变量 用在 docker-compose 里面使用, 尽量自己调试一遍后再使用"

!!! tip ""
    ```sh
    git clone https://github.com/jumpserver/Dockerfile.git
    cd Dockerfile
    cp config_example.conf .env
    cat .env
    docker-compose up
    ```

!!! tip "[仓库地址](https://github.com/jumpserver/Dockerfile)"

!!! tip "后续的使用请参考 [安全建议](install_security.md) [快速入门](../../admin-guide/quick_start/)"
