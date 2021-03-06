# 安装文档

!!! warning "提示"
    推荐使用 [极速安装](setup_by_fast.md) 快速部署，资产规模较大参考 [分布式部署](setup_by_prod.md) 进行部署  
    本文档需要非常强的动手能力, 部署过程中你会面临各种各样的问题  

    注意: 使用本文档你将无法获得额外的技术支持，包括后续的升级均需要自行处理，我们只推荐真正有需要的运维工程师进行使用

!!! info "本文档是针对所有 `Linux` 发行版 `x86_64` 的安装说明, 非特定系统说明文档, 但是示例中我们仅展示 `Ubuntu` 和` Centos` 部分(注释部分)"
    - 遇到问题可以参考 [安装视频](https://www.bilibili.com/video/BV1VV411C797)

!!! info "JumpServer 环境要求:"
    硬件配置: 2个CPU核心, 4G 内存, 50G 硬盘（最低）  
    操作系统: Linux 发行版 x86_64  

    Python = 3.6.x  
    Mysql Server ≥ 5.6  
    Mariadb Server ≥ 5.5.56  
    Redis

## 安装步骤

### 1. 安装 Python3.6 MySQL Redis

!!! tip ""
    推荐直接从仓库获取

!!! tip "数据库字符集要求:"
    ```mysql
    create database jumpserver default charset 'utf8' collate 'utf8_bin';
    ```

### 2. 创建 Python 虚拟环境

!!! tip ""
    ```sh
    python3.6 -m venv /opt/py3
    ```

### 3. 载入 Python 虚拟环境

!!! tip ""
    ```sh
    source /opt/py3/bin/activate
    ```

!!! tip "每次操作 JumpServer 都需要先载入 py3 虚拟环境"  
    ??? warning "部分系统可能会提示 source: not found, 可以使用 . 代替 source"
        ```sh
        . /opt/py3/bin/activate  
        ```
        可以在 ~/.bashrc 末尾加入 source /opt/py3/bin/activate 自动载入环境


### 4. 获取 JumpServer 代码

!!! tip ""
    ```sh
    cd /opt && \
    wget https://github.com/jumpserver/jumpserver/releases/download/v2.3.0/jumpserver-v2.3.0.tar.gz
    ```

!!! tip ""
    ```sh
    tar xf jumpserver-v2.3.0.tar.gz
    mv jumpserver-v2.3.0 jumpserver
    ```

### 5. 安装编译环境依赖

!!! tip ""
    ```sh
    cd /opt/jumpserver/requirements
    ```

??? tip "根据当前系统, 选择对应的文件执行即可"
    Centos:
    ```sh
    yum install -y $(cat rpm_requirements.txt)
    ```
    Ubuntu:
    ```sh
    apt-get install -y $(cat deb_requirements.txt)
    ```

!!! tip ""
    ```sh
    pip install wheel && \
    pip install --upgrade pip setuptools && \
    pip install -r requirements.txt
    ```

??? question "确保已经载入 py3 虚拟环境, 中间如果遇到报错一般是依赖包没装全, 可以通过 搜索引擎 解决"
    国内可以使用镜像加速  
    ```sh
    pip install wheel -i https://mirrors.aliyun.com/pypi/simple/
    pip install --upgrade pip setuptools -i https://mirrors.aliyun.com/pypi/simple/
    pip install -r requirements.txt -i https://mirrors.aliyun.com/pypi/simple/
    ```

### 6. 修改配置文件

!!! tip ""
    ```sh
    cd /opt/jumpserver && \
    cp config_example.yml config.yml && \
    vi config.yml
    ```

??? info "注意不能使用纯数字字符串, 可以参考此模版"
    ```yaml
    # SECURITY WARNING: keep the secret key used in production secret!
    # 加密秘钥 生产环境中请修改为随机字符串，请勿外泄, 可使用命令生成
    # cat /dev/urandom | tr -dc A-Za-z0-9 | head -c 49;echo
    SECRET_KEY: W5Ic3fMXNZ0p5RIy5DhJYJllppTfcfkW8Yuf94VBMfpcssbfu

    # SECURITY WARNING: keep the bootstrap token used in production secret!
    # 预共享Token coco和guacamole用来注册服务账号，不在使用原来的注册接受机制
    BOOTSTRAP_TOKEN: zxffNymGjP79j6BN

    # Development env open this, when error occur display the full process track, Production disable it
    # DEBUG 模式 开启DEBUG后遇到错误时可以看到更多日志
    DEBUG: false

    # DEBUG, INFO, WARNING, ERROR, CRITICAL can set. See https://docs.djangoproject.com/en/1.10/topics/logging/
    # 日志级别
    LOG_LEVEL: ERROR
    # LOG_DIR:

    # Session expiration setting, Default 24 hour, Also set expired on on browser close
    # 浏览器Session过期时间，默认24小时, 也可以设置浏览器关闭则过期
    # SESSION_COOKIE_AGE: 86400
    SESSION_EXPIRE_AT_BROWSER_CLOSE: true

    # Database setting, Support sqlite3, mysql, postgres ....
    # 数据库设置
    # See https://docs.djangoproject.com/en/1.10/ref/settings/#databases

    # SQLite setting:
    # 使用单文件sqlite数据库
    # DB_ENGINE: sqlite3
    # DB_NAME:

    # MySQL or postgres setting like:
    # 使用Mysql作为数据库
    DB_ENGINE: mysql
    DB_HOST: 127.0.0.1
    DB_PORT: 3306
    DB_USER: jumpserver
    DB_PASSWORD: rBi41SrDqlX4zsx9e1L0cqTP
    DB_NAME: jumpserver

    # When Django start it will bind this host and port
    # ./manage.py runserver 127.0.0.1:8080
    # 运行时绑定端口
    HTTP_BIND_HOST: 0.0.0.0
    HTTP_LISTEN_PORT: 8080
    WS_LISTEN_PORT: 8070

    # Use Redis as broker for celery and web socket
    # Redis配置
    REDIS_HOST: 127.0.0.1
    REDIS_PORT: 6379
    REDIS_PASSWORD: ZhYnLrodpmPncovxJTnRyiBs
    # REDIS_DB_CELERY: 3
    # REDIS_DB_CACHE: 4

    # Use OpenID authorization
    # 使用OpenID 来进行认证设置
    # BASE_SITE_URL: http://localhost:8080
    # AUTH_OPENID: false  # True or False
    # AUTH_OPENID_SERVER_URL: https://openid-auth-server.com/
    # AUTH_OPENID_REALM_NAME: realm-name
    # AUTH_OPENID_CLIENT_ID: client-id
    # AUTH_OPENID_CLIENT_SECRET: client-secret
    # AUTH_OPENID_IGNORE_SSL_VERIFICATION: True
    # AUTH_OPENID_SHARE_SESSION: True

    # Use Radius authorization
    # 使用Radius来认证
    # AUTH_RADIUS: false
    # RADIUS_SERVER: localhost
    # RADIUS_PORT: 1812
    # RADIUS_SECRET:

    # CAS 配置
    # AUTH_CAS': False,
    # CAS_SERVER_URL': "http://host/cas/",
    # CAS_ROOT_PROXIED_AS': 'http://jumpserver-host:port',  
    # CAS_LOGOUT_COMPLETELY': True,
    # CAS_VERSION': 3,

    # LDAP/AD settings
    # LDAP 搜索分页数量
    # AUTH_LDAP_SEARCH_PAGED_SIZE: 1000
    #
    # 定时同步用户
    # 启用 / 禁用
    # AUTH_LDAP_SYNC_IS_PERIODIC: True
    # 同步间隔 (单位: 时) (优先）
    # AUTH_LDAP_SYNC_INTERVAL: 12
    # Crontab 表达式
    # AUTH_LDAP_SYNC_CRONTAB: * 6 * * *
    #
    # LDAP 用户登录时仅允许在用户列表中的用户执行 LDAP Server 认证
    # AUTH_LDAP_USER_LOGIN_ONLY_IN_USERS: False
    #
    # LDAP 认证时如果日志中出现以下信息将参数设置为 0 (详情参见：https://www.python-ldap.org/en/latest/faq.html)
    # In order to perform this operation a successful bind must be completed on the connection
    # AUTH_LDAP_OPTIONS_OPT_REFERRALS: -1

    # OTP settings
    # OTP/MFA 配置
    # OTP_VALID_WINDOW: 0
    # OTP_ISSUER_NAME: Jumpserver

    # Perm show single asset to ungrouped node
    # 是否把未授权节点资产放入到 未分组 节点中
    # PERM_SINGLE_ASSET_TO_UNGROUP_NODE: false
    #
    # 启用定时任务
    # PERIOD_TASK_ENABLE: True
    #
    # 启用二次复合认证配置
    # LOGIN_CONFIRM_ENABLE: False
    #
    # Windows 登录跳过手动输入密码
    WINDOWS_SKIP_ALL_MANUAL_PASSWORD: True
    ```

### 7. 启动 JumpServer

!!! tip ""
    ```sh
    cd /opt/jumpserver
    ./jms start
    ```

??? warning "确保已经载入 py3 虚拟环境"
    ```sh
    source /opt/py3/bin/activate
    ```

??? tip "可以 -d 参数在后台运行"
    ```sh
    ./jms start -d
    ```

### 8. 正常部署 KoKo 组件

!!! tip ""
    ```sh
    cd /opt && \
    wget https://github.com/jumpserver/koko/releases/download/v2.3.0/koko-v2.3.0-linux-amd64.tar.gz
    ```

!!! tip ""
    ```sh                               
    tar -xf koko-v2.3.0-linux-amd64.tar.gz && \
    mv koko-v2.3.0-linux-amd64 koko && \
    chown -R root:root koko && \
    cd koko \
    mv kubectl /usr/local/bin/ && \
    wget https://download.jumpserver.org/public/kubectl.tar.gz && \
    tar -xf kubectl.tar.gz && \
    chmod 755 kubectl && \
    mv kubectl /usr/local/bin/rawkubectl && \
    rm -rf kubectl.tar.gz
    ```

!!! tip ""
    ```sh
    cp config_example.yml config.yml && \
    vi config.yml
    ```

??? info "BOOTSTRAP_TOKEN 需要从 jumpserver/config.yml 里面获取, 保证一致"
    以下配置仅供参考
    ```yaml
    # 项目名称, 会用来向Jumpserver注册, 识别而已, 不能重复
    # NAME: {{ Hostname }}

    # Jumpserver项目的url, api请求注册会使用
    CORE_HOST: http://127.0.0.1:8080

    # Bootstrap Token, 预共享秘钥, 用来注册coco使用的service account和terminal
    # 请和jumpserver 配置文件中保持一致，注册完成后可以删除
    BOOTSTRAP_TOKEN: zxffNymGjP79j6BN

    # 启动时绑定的ip, 默认 0.0.0.0
    # BIND_HOST: 0.0.0.0

    # 监听的SSH端口号, 默认2222
    # SSHD_PORT: 2222

    # 监听的HTTP/WS端口号，默认5000
    # HTTPD_PORT: 5000

    # 项目使用的ACCESS KEY, 默认会注册,并保存到 ACCESS_KEY_STORE中,
    # 如果有需求, 可以写到配置文件中, 格式 access_key_id:access_key_secret
    # ACCESS_KEY: null

    # ACCESS KEY 保存的地址, 默认注册后会保存到该文件中
    # ACCESS_KEY_FILE: data/keys/.access_key

    # 设置日志级别 [DEBUG, INFO, WARN, ERROR, FATAL, CRITICAL]
    LOG_LEVEL: ERROR

    # SSH连接超时时间 (default 15 seconds)
    # SSH_TIMEOUT: 15

    # 语言 [en,zh]
    # LANG: zh

    # SFTP的根目录, 可选 /tmp, Home其他自定义目录
    # SFTP_ROOT: /tmp

    # SFTP是否显示隐藏文件
    # SFTP_SHOW_HIDDEN_FILE: false

    # 是否复用和用户后端资产已建立的连接(用户不会复用其他用户的连接)
    # REUSE_CONNECTION: true

    # 资产加载策略, 可根据资产规模自行调整. 默认异步加载资产, 异步搜索分页; 如果为all, 则资产全部加载, 本地搜索分页.
    # ASSET_LOAD_POLICY:

    # zip压缩的最大额度 (单位: M)
    # ZIP_MAX_SIZE: 1024M

    # zip压缩存放的临时目录 /tmp
    # ZIP_TMP_PATH: /tmp

    # 向 SSH Client 连接发送心跳的时间间隔 (单位: 秒)，默认为30, 0则表示不发送
    # CLIENT_ALIVE_INTERVAL: 30

    # 向资产发送心跳包的重试次数，默认为3
    # RETRY_ALIVE_COUNT_MAX: 3

    # 会话共享使用的类型 [local, redis], 默认local
    SHARE_ROOM_TYPE: redis

    # Redis配置
    REDIS_HOST: 127.0.0.1
    REDIS_PORT: 6379
    REDIS_PASSWORD: ZhYnLrodpmPncovxJTnRyiBs
    # REDIS_CLUSTERS:
    REDIS_DB_ROOM: 6
    ```

!!! tip ""
    ```sh
    ./koko  
    ```

??? tip "可以 -d 参数在后台运行"
    ```sh
    ./koko -d
    ```

### 8.1. Docker 部署 KoKo 组件

??? info "如果前面已经正常部署了 KoKo, 可以跳过此步骤"
    ```sh
    docker run --name jms_koko -d \
      -p 2222:2222 -p 127.0.0.1:5000:5000 \
      -e CORE_HOST=http://<Jumpserver_url> \
      -e BOOTSTRAP_TOKEN=<Jumpserver_BOOTSTRAP_TOKEN> \
      -e LOG_LEVEL=ERROR \
      --restart=always \
      --privileged=true \
      jumpserver/jms_koko:<Tag>
    <Jumpserver_url> 为 jumpserver 的 url 地址, <Jumpserver_BOOTSTRAP_TOKEN> 需要从 jumpserver/config.yml 里面获取, 保证一致, <Tag> 是版本
    ```

!!! tip "例:"
    ```sh
    docker run --name jms_koko -d \
      -p 2222:2222 \
      -p 127.0.0.1:5000:5000 \
      -e CORE_HOST=http://192.168.244.144:8080 \
      -e BOOTSTRAP_TOKEN=zxffNymGjP79j6BN \
      -e LOG_LEVEL=ERROR \
      --privileged=true \
      --restart=always \
      jumpserver/jms_koko:v2.3.0
    ```

### 9. 正常部署 Guacamole 组件

!!! tip "建议使用 Docker 部署 Guacamole 组件 , 部分环境可能无法正常编译安装"

!!! tip ""
    ```sh
    cd /opt && \
    wget -O docker-guacamole-v2.3.0.tar.gz https://github.com/jumpserver/docker-guacamole/archive/master.tar.gz
    ```

!!! tip ""
    ```sh
    mkdir /opt/docker-guacamole && \
    tar -xf docker-guacamole-v2.3.0.tar.gz -C /opt/docker-guacamole --strip-components 1 && \
    rm -rf /opt/docker-guacamole-v2.3.0.tar.gz && \
    cd /opt/docker-guacamole && \
    wget http://download.jumpserver.org/public/guacamole-server-1.2.0.tar.gz && \
    tar -xf guacamole-server-1.2.0.tar.gz && \
    wget http://download.jumpserver.org/public/ssh-forward.tar.gz && \
    tar -xf ssh-forward.tar.gz -C /bin/ && \
    chmod +x /bin/ssh-forward
    ```

!!! tip ""
    ```sh
    cd /opt/docker-guacamole/guacamole-server-1.2.0
    ```

!!! warning "根据 [Guacamole官方文档](http://guacamole.apache.org/doc/gug/installing-guacamole.html) 文档安装对应的依赖包"

!!! tip ""
    ```sh
    ./configure --with-init-dir=/etc/init.d && \
    make && \
    make install
    ```

??? warning "需要先在当前环境配置好 Java"
    Ubuntu:  
    ```sh
    apt-get -y install default-jre default-jdk
    ```
    Centos:  
    ```sh
    yum install -y java-1.8.0-openjdk
    ```

!!! tip ""
    ```sh
    mkdir -p /config/guacamole /config/guacamole/extensions /config/guacamole/record /config/guacamole/drive && \
    chown daemon:daemon /config/guacamole/record /config/guacamole/drive && \
    cd /config
    ```

??? warning "访问 [此处](https://tomcat.apache.org/download-90.cgi) 下载最新的 Tomcat9"
    !!! question "网络有问题可以通过国内镜像源下载"
    ```sh
    wget http://mirrors.tuna.tsinghua.edu.cn/apache/tomcat/tomcat-9/v9.0.38/bin/apache-tomcat-9.0.38.tar.gz
    ```

!!! tip ""
    ```sh
    tar -xf apache-tomcat-9.0.36.tar.gz && \
    mv apache-tomcat-9.0.36 tomcat9 && \
    rm -rf /config/tomcat9/webapps/* && \
    sed -i 's/Connector port="8080"/Connector port="8081"/g' /config/tomcat9/conf/server.xml && \
    echo "java.util.logging.ConsoleHandler.encoding = UTF-8" >> /config/tomcat9/conf/logging.properties && \
    wget http://download.jumpserver.org/release/v2.3.0/guacamole-client-v2.3.0.tar.gz && \
    tar -xf guacamole-client-v2.3.0.tar.gz && \
    rm -rf guacamole-client-v2.3.0.tar.gz && \
    cp guacamole-client-v2.3.0/guacamole-*.war /config/tomcat9/webapps/ROOT.war && \
    cp guacamole-client-v2.3.0/guacamole-*.jar /config/guacamole/extensions/ && \
    mv /opt/docker-guacamole/guacamole.properties /config/guacamole/ && \
    rm -rf /opt/docker-guacamole && \
    ```

!!! warning "设置 Guacamole 环境"
    ```sh
    export JUMPSERVER_SERVER=http://127.0.0.1:8080
    echo "export JUMPSERVER_SERVER=http://127.0.0.1:8080" >> ~/.bashrc
    export BOOTSTRAP_TOKEN=zxffNymGjP79j6BN
    echo "export BOOTSTRAP_TOKEN=zxffNymGjP79j6BN" >> ~/.bashrc
    export JUMPSERVER_KEY_DIR=/config/guacamole/data/keys
    echo "export JUMPSERVER_KEY_DIR=/config/guacamole/data/keys" >> ~/.bashrc
    export GUACAMOLE_HOME=/config/guacamole
    echo "export GUACAMOLE_HOME=/config/guacamole" >> ~/.bashrc
    export GUACAMOLE_LOG_LEVEL=ERROR
    echo "export GUACAMOLE_LOG_LEVEL=ERROR" >> ~/.bashrc
    export JUMPSERVER_ENABLE_DRIVE=true
    echo "export JUMPSERVER_ENABLE_DRIVE=true" >> ~/.bashrc
    ```

??? info "环境变量说明"
    JUMPSERVER_SERVER 指 core 访问地址  
    BOOTSTRAP_TOKEN 为 Jumpserver/config.yml 里面的 BOOTSTRAP_TOKEN 值  
    JUMPSERVER_KEY_DIR 认证成功后 key 存放目录  
    GUACAMOLE_HOME 为 guacamole.properties 配置文件所在目录  
    GUACAMOLE_LOG_LEVEL 为生成日志的等级  
    JUMPSERVER_ENABLE_DRIVE 为 rdp 协议挂载共享盘

!!! tip ""
    ```sh
    /etc/init.d/guacd start
    sh /config/tomcat9/bin/startup.sh
    ```

### 9.1 Docker 部署 Guacamole 组件

!!! tip "如果前面已经正常部署了 Guacamole, 可以跳过此步骤"
    ```sh
    docker run --name jms_guacamole -d \
      -p 127.0.0.1:8081:8080 \
      -e JUMPSERVER_SERVER=http://<Jumpserver_url> \
      -e BOOTSTRAP_TOKEN=<Jumpserver_BOOTSTRAP_TOKEN> \
      -e GUACAMOLE_LOG_LEVEL=ERROR \
      jumpserver/jms_guacamole:<Tag>
    <Jumpserver_url> 为 JumpServer 的 url 地址, <Jumpserver_BOOTSTRAP_TOKEN> 需要从 jumpserver/config.yml 里面获取, 保证一致, <Tag> 是版本
    ```

!!! tip "例:"
    ```sh
    docker run --name jms_guacamole -d \
      -p 127.0.0.1:8081:8080 \
      -e JUMPSERVER_SERVER=http://192.168.244.144:8080 \
      -e BOOTSTRAP_TOKEN=abcdefg1234 \
      -e GUACAMOLE_LOG_LEVEL=ERROR \
      jumpserver/jms_guacamole:v2.3.0
    ```

### 10. 下载 Lina 组件

!!! tip ""
    ```sh
    cd /opt
    wget https://github.com/jumpserver/lina/releases/download/v2.3.0/lina-v2.3.0.tar.gz
    ```

!!! tip ""
    ```sh
    tar -xf lina-v2.3.0.tar.gz
    mv lina-v2.3.0 lina
    chown -R nginx:nginx lina
    ```


### 11. 下载 Luna 组件

!!! tip ""
    ```sh
    cd /opt
    wget https://github.com/jumpserver/luna/releases/download/v2.3.0/luna-v2.3.0.tar.gz
    ```

!!! tip ""
    ```sh
    tar -xf luna-v2.3.0.tar.gz
    mv luna-v2.3.0 luna
    chown -R nginx:nginx luna
    ```

### 12. 配置 Nginx 整合各组件

!!! tip "参考 [官方文档](http://nginx.org/en/linux_packages.html) 安装最新的稳定版 nginx"

!!! tip ""
    ```sh
    echo > /etc/nginx/conf.d/default.conf
    vi /etc/nginx/conf.d/jumpserver.conf
    ```

!!! tip ""
    ```vim
    server {
        listen 80;

        client_max_body_size 100m;  # 录像及文件上传大小限制

        location /ui/ {
            try_files $uri / /index.html;
            alias /opt/lina/;
        }

        location /luna/ {
            try_files $uri / /index.html;
            alias /opt/luna/;  # luna 路径, 如果修改安装目录, 此处需要修改
        }

        location /media/ {
            add_header Content-Encoding gzip;
            root /opt/jumpserver/data/;  # 录像位置, 如果修改安装目录, 此处需要修改
        }

        location /static/ {
            root /opt/jumpserver/data/;  # 静态资源, 如果修改安装目录, 此处需要修改
        }

        location /koko/ {
            proxy_pass       http://localhost:5000;
            proxy_buffering off;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            access_log off;
        }

        location /guacamole/ {
            proxy_pass       http://localhost:8081/;
            proxy_buffering off;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection $http_connection;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            access_log off;
        }

        location /ws/ {
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_pass http://localhost:8070;
            proxy_http_version 1.1;
            proxy_buffering off;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
        }

        location /api/ {
            proxy_pass http://localhost:8080;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location /core/ {
            proxy_pass http://localhost:8080;
            proxy_set_header X-Real-IP $remote_addr;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location / {
            rewrite ^/(.*)$ /ui/$1 last;
        }
    }
    ```

!!! tip ""
    ```sh
    nginx -t
    nginx -s reload
    ```

### 13. 开始使用 JumpServer

!!! tip "检查应用是否已经正常运行"
    服务全部启动后, 访问 JumpServer 服务器 nginx 代理的 80 端口, 不要通过8080端口访问
    默认账号: admin 密码: admin  


后续的使用请参考 [安全建议](install_security.md) [快速入门](../../admin-guide/quick_start/)
