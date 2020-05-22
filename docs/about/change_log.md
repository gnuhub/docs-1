# 更新日志

1.5.9
------------------------
2020年05月21日

- [新版 OpenID Connect 认证配置文档](../../admin-guide/authentication/openid/)
- [下载离线播放器](https://github.com/jumpserver/VideoPlayer/releases/)
- [申请试用JumpServer 企业版](https://jinshuju.net/f/kyOYpi/)

!!! note "新增功能"

* 支持标准 OpenID Connect

!!! summary "优化功能"

* 优化仪表盘加载速度
* 优化资产查询速度
* 更新云管中心中各云服务提供商支持的地域列表（比如：阿里云-西南1）【XPack】
* 优化连接日志信息
* 调整TreeAPI请求地址
* 添加支持直接连接数据库应用

!!! success "修复Bug"

* 修复MFA二次认证的异常问题
* 修复API Key不能删除的问题
* 修复多组织下仪表盘数据显示不准确问题
* 修复FTP日志没有按照组织进行存放的问题
* 修复用户授权资产树及列表数据显示不稳定问题
* 修复用户页面更新MFA时解除管理员强制启用的问题
* 修复任务列表执行历史中统计数据显示不准确的问题
* 修复资产授权用户/用户组页面删除用户组失败的问题
* 修复右击资产树点击仅显示当前节点下资产不生效的问题
* 修复授权模块的信号处理器由于不能正常监控而导致的系统用户不能自动推送到资产以及没有关联资产的问题
* 修复连接资产无反应问题

!!! info "升级依赖"

* jumpserver-django-oidc-rp==0.3.7.4

1.5.8
------------------------
2020年04月16日

- [下载离线播放器](https://github.com/jumpserver/VideoPlayer)
- [申请试用 JumpServer 企业版](https://jinshuju.net/f/kyOYpi/)

!!! note "新增功能"

* 在线会话监控（备注：目前仅支持协议类型为ssh、telnet、mysql的在线会话）
* 批量改密（支持修改root、administrator等特殊用户）【XPack】
* 创建云管中心同步实例任务时，可选择是否覆盖同步的资产信息【XPack】
* 新增在线会话监控【koko】

!!! summary "优化功能"

* 创建录像存储时自动清除空白字符
* 修改中间件中获取当前组织的优先级
* 更新播放器下载地址链接
* 优化创建AuthBook逻辑（添加互斥锁机制）
* 修改组织获取优先级
* 禁用ansible的ssh连接复用
* 修改项目使用的cache default(redis_cache -> redis_lock)
* 更新用户时显示CAS用户来源选项

!!! success "修复Bug"

* 修复列表中日期显示问题
* 修复资产用户列表删除失败的问题
* 修复命令记录导出问题（导出满足搜索条件的命令记录）
* 修复因数据不支持timezone引起的仪表盘数据为空的问题
* 修复自定义平台列表在详情页删除失败的问题
* 修复命令记录/操作/改密日志搜索字段没清空的问题
* 修复系统设置-终端设置-资产排序设置不生效的问题
* 修复点击测试邮件后，配置信息获取不稳定的问题
* 修复使用容器时，Azure录像上传问题（ 镜像添加ca-certificates依赖 ）【koko】

!!! info "更新依赖"

* python-redis-lock==3.5.0
* jms-storage-sdk==0.0.29

1.5.7
------------------------
2020年3月19日

- [JumpServer 录像离线播放器](https://github.com/jumpserver/VideoPlayer)

!!! note "新增功能"

* 支持 CAS Server （中央认证服务）用户登录认证
* 提出动态系统用户的概念，当用户登录资产时自动使用与其 JumpServer用户名相同的系统用户连接资产
* 自定义配置文件上传路径，允许管理员为不同系统用户指定不同的SFTP挂载目录，目前仅支持Linux资产
* 支持下载会话录像，可配合JumpServer Video Player 进行离线播放，并附带录像的操作信息，JumpServer Video Player 适配 Mac 、Windows 和 Linux
* 云管中心支持同步华为云实例；对云上已释放实例进行本地标记 【XPack】
* 批量改密针对特殊用户（如root、administrator等）开放改密操作【XPack】
* 支持动态的系统用户名
* 增加命令记录风险标记
* 增加用户 SSH 连接心跳设置，默认30s
* 隔离 MySql 连接的进程空间

!!! summary "优化功能"


* 优化Dashboard页面加载速度
* 优化MFA登录页面
* 优化资产授权规则，当用户、用户组、资产、节点、系统用户等变更时，实时刷新与其他实体之间的关联关系
* 优化资产用户列表展示和API性能优化
* 优化LDAP/AD配置模块的测试可连接性逻辑，并添加测试用户登录的功能
* 优化可连接性测试逻辑
* 优化部分API（包括资产、系统用户、管理用户等相关API）处理逻辑
* 优化改密计划执行流程【XPack】
* 增强 SSH Client 复用连接，免受 SSH MaxSessions 限制
* 增强 Websocket 连接处理能力
* 增强 Web 文件管理功能，支持软连接目录，增加错误信息提示
* 增强 SFTP 功能，根目录可依据系统用户动态配置
* 增强 Telnet Client 连接
* 录像存储配置动态更新

!!! success "修复Bug"

* 修复无法删除空节点的问题
* 修复命令记录、批量命令没有针对组织进行分组显示的问题
* 修复存在无效 ES 存储时访问命令记录页面失效的问题
* 修复会对第三方认证用户发送创建用户成功邮件、密码过期提醒邮件的问题
* 修复部分pip依赖包版本不兼容的问题
* 修复 Telnet 资产网关连接未关闭问题
* 修复主进程假死问题
* 修复首次启动获取录像存储类型为 Null 的问题

1.5.6
------------------------
2020年1月2日

!!! info "漏洞修复"

* 修复用户被强制开启使用 MFA 二次认证后可以自主绕过绑定的问题

!!! note "新增功能"

* 全面支持 IPv6
* 数据库应用【商业版】
* Windows 批量命令
* 录像存储类型：Swift、Ceph
* 节点详情（右击节点显示）
* 资产平台列表

!!! summary "优化功能"

* 录像/命令存储配置迁移到 Terminal 模块
* 优化用户详情页面
* 用户列表添加移除操作（非DEFAULT组织）【商业版】
* 用户第三方认证后，只在创建时修改用户来源信息
* 优化前端 Form 渲染逻辑（存储配置、RemoteApp、DatabaseApp）
* 统一导入导出组件
* 统一了树列表基础模板
* 优化日志审计（操作日志，改密日志）
* API 采用 serializer_classes 字段（default, display）
* 统一系统配置的 Tab 切换
* 统一没有nav的页面（重置密码，忘记密码，重置中设置密码，独立 message 页面）
* 优化用户组列表页（不返回组中用户，只返回数量）
* 组织的一些方法变为layzproperty，避免重复计算
* 用户组增加删除用户（用户组详情页）
* 优化Ops Task表结构，减少数据库查询次数
* 优化基础的 Encryptjsonfield
* 修改 Adhoc 返回的 become 字段，避免密码泄露
* 修改校验用户资产权限API不使用缓存
* 用户登录日志，采用同步机制
* 右击节点菜单位置计算
* 命令存储（ES）相关字段设置为 required
* 操作日志文案，用户修改为操作者
* 调整 Web 文件管理为节点树结构
* 支持 Web 文件管理的资产搜索
* 增加 SSH 连接的加密算法以支持旧设备

!!! success "修复Bug"

* 检验用户有效性逻辑（解决启用LDAP等认证时，显示用户名不存在）
* 工单按用户搜索无效的问题
* 密码匣子选择 id 导出时的问题
* 解决密码匣子翻页再次选择资产时不能设置到选择框的问题
* 解决管理员重置用户MFA后，自动退出的问题
* 修复无法使用中文搜索资产
* 修复因自定义正则造成的程序异常
* 修复因S3配置造成的程序异常
* 优化部分代码

!!! info "更新依赖"

* psutil==5.6.5
* go-elasticsearch v6.8.5

1.5.5
------------------------
2019年12月4日

!!! note "新增功能"

* 工单管理【商业版】
* 二次复合（用户登录）【商业版】
* 二次认证（MFA Radius）
* 重启后支持自动上传遗留录像
* 支持 Windows 连接超时断开

!!! summary "优化功能"

* LDAP/AD 逻辑
* 可修改用户来源（用户创建）
* 收集资产用户（显示用户最后登录时间）
* 左侧组织增加搜索过滤
* 可关闭页面提示信息
* 资产用户列表支持模糊搜索
* 跳过手动输入密码配置（Windows）
* 优化授权资产分页展示
* 支持授权资产的多级搜索
* 支持用户登录的二次审核

!!! success "修复Bug"

* 修复用户授权资产问题（用户组/用户授权变更刷新问题）
* 修复因版本不一致造成的异常
* 修复部分 telnet 登录问题

1.5.4
------------------------
2019年10月23日

!!! note "新增功能"

* 用户收藏资产（用户页面 -> 我的资产）
* LDAP 登录认证添加配置项：只有在用户列表中的用户会被允许认证（配置项可在 config_example.yml 中查找 AUTH_LDAP_USER_LOGIN_ONLY_IN_USERS）

!!! summary "优化功能"

* 优化 LDAP 用户导入/搜索的逻辑（采用用户过滤器方式）
* 优化命令列表中命令的显示（解决命令太长的问题）
* 优化 select2 js/css 依赖版本(4.0.10)（解决多选下拉框自动回跳到顶部的问题）
* 优化 celery log 显示（采用 Websocket 方式）
* 优化节点删除 API，返回删除失败原因（包含子节点或资产）
* 限制系统用户 name 字段使用特殊字符
* 添加脚本：get_no_parent_nodes.py
* 更新创建/更新用户组的取消按钮->重置按钮（避免引起歧义）
* 优化所有 API 的 get_queryset 方式
* 修改获取系统用户 API 为只返回节点数量（之前是返回节点列表）
* 修改 session 支持 protocol 搜索
* 修改 form serializer 对应的多对多字段
* 修改命令批量执行左侧选择系统用户
* 修改查看资产用户 Auth info 可配置关闭 MFA 校验
* 优化创建用户邮件内容
* 优化用户组详情页面选择用户下拉列表使用异步加载
* 优化命令过滤详情绑定到系统用户点击下拉框自动关闭的问题
* 优化提交 api 报错时滚动到错误提示行
* 优化 table 页面某些列宽度
* 修改 jms 启动脚本，stop 时增加超时检测
* 修改导出登录日志的日期选择从开始日期的00:00:00，到结束日期的23:59:59
* 修改返回资产树包含组织信息
* 限制组织名称中使用的特殊字符【X-pack 企业版】

!!! success "修复Bug"

* 修复调用系统用户资产 API 时 Connectivity is not JSON serializable 的 Bug
* 修复命令记录从 es 中获取失败（原因：时间日期格式不匹配）
* 修改终端命令类型 MAPPING（elasticsearch -> es）
* 修复资产授权列表搜索 invalid:false 时出现 500 错误
* 修复导出资产 csv 文件为空的问题
* 修复导致 favorite 和 empty 同时出现的问题
* 修复读取日志时可能解码失败的问题
* 修复组织管理员在资产详情页面不显示（删除/更新）按钮的问题【X-pack 企业版】
* 修复组织管理员查看用户权限失败问题【X-pack 企业版】

!!! info "更新依赖"

* select2 升级版本 4.0.10（解决多选下拉框选择跳到顶部的问题）

1.5.3
------------------------
2019年9月24日

!!! info "组件说明"

* 自 v1.5.3 版本起（包含 v1.5.3） ，Koko 将担任 Coco 在 JumpServer 项目中的重要角色，之后的版本将不会再对 Coco 进行升级维护。

!!! note "新增功能"

* 添加页面创建 API Key 的功能（右上角点击账号下拉列表 -> API Key）
* 在线会话列表中允许终断 RDP Session
* 添加用户树缓存

!!! summary "优化功能"

* 优化资产树加载逻辑
* 优化资产授权树、授权规则加载、过滤逻辑
* 优化前端 asset modal table
* 统一 URL 地址
* 修改 Swagger
* 允许批量删除用户，修改前端提示信息逻辑
* 推送系统用户时，在资产上创建同名的用户组
* 资产协议修改：telnet (beta) => telnet
* WebTerminal 跳转时添加时间戳

!!! success "修复Bug"

* 修复授权规则列表同一条数据重复显示的问题
* 修复授权规则列表翻页后重复展示前几页中数据的问题
* 修复授权详情中授权资产或节点添加资产失败的问题
* 修复系统设置的配置偶尔不生效的问题
* 修复命令执行左侧树点击问题
* 修复用户认证序列类获取 request 的问题
* 修复批量创建系统用户等资源时，initial_data 获取数据失败的问题
* 修复创建授权规则授权节点时，系统用户不自动推送的问题
* 修复浏览器关闭后 Session 不失效的问题
* 解决授权了一个节点，当移动节点后，被移动的节点下的资产会放到未分组节点下的问题
* 修复刷新资产硬件信息时无法检测 NVMe 的硬盘的问题
* 解决命令执行宽度问题

!!! info "更新依赖"

* 升级 jQuery v3.1.1

1.5.2
------------------------
2019年7月16日

!!! note "新增功能"

* 系统设置-安全设置中添加配置项：终端注册

!!! summary "优化功能"

* 获取系统用户授权资产时，只返回资产协议支持的系统用户。
* 表单使用API进行提交
* 优化授权规则资产列表页面
* 在线/历史会话页面去掉协议搜索选项

!!! success "修复Bug"

* 解决命令过滤器详情添加系统用户失败的问题
* 解决命令过滤器详情页删除功能不可用的问题
* 解决可以创建同名命令过滤器的问题（修复资产授权详情页删除弹出框的权限名显示不对)
* 解决在资产授权详情页删除授权规则时弹出框中名称显示不正确的问题
* 解决网域详情页删除功能不可用的问题
* 解决资产列表数量显示不正确的问题
* 解决创建命令过滤规则类型为正则表达式时创建不成功的问题
* 解决授权规则详情用户组数量显示不正确的问题
* 解决日期显示差8小时的问题
* 解决创建资产失败的问题（原因：协议的添加、删除逻辑）
* 解决授权页面不显示资产的问题
* 解决授权资产包含已禁用资产的问题
* 解决系统用户、管理用户提交会重置密码的问题
* 解决批量执行命令没有选择资产的问题

1.5.1
------------------------
2019年7月6日

!!! note "新增功能"

* 审计员（用户添加审计员角色）

!!! summary "优化功能"

* 用户页面优化资产标签过滤功能
* 用户创建添加到当前组织（API调用）
* 资产授权树显示策略（将单独授权的资产添加到自定义的默认节点下）
* 资产创建支持添加多个协议
* 资产创建设置节点策略（API/CSV, 解决总是会添加到默认节点的问题）
* 邮件设置添加发送账号选项（解决SMTP账号和发送账号不一致的问题）
* 安全设置添加批量命令选项（解决禁止普通用户批量执行命令的问题）
* 终端(coco/guacamole)上报Session/FTP用户信息使用 name（username）格式
* Windows资产可通过SSH协议连接
* Windows资产支持直接复制粘贴文本（浏览器授权剪切板权限）
* 添加一键禁用LDAP认证脚本
* 解决连接windows资产出现幽灵会话的问题
* 优化创建授权规则时，授权动作的展示
* 解决操作日志中出现coco/guamole更新Default节点的问题
* 优化命令记录列表/在线/历史会话列表（提高响应速度，取消返回所有资产）

!!! success "修复Bug"

* 修复文件导出使用excel打开乱码的问题
* 解决用户授权资产/节点为空时，前端构建资产授权树的Bug

1.5.0
------------------------
2019年5月29日

!!! note "新增功能"

* 支持启用MFA的管理员查看资产用户密码
* 可自定义创建用户时发送创建用户成功的邮件内容
* 创建用户时，可选择用户密码设置策略(可解决客户没有邮件系统的场景)
* (用户/用户组/资产/管理用户/系统用户)资源支持使用csv文件类型进行导入、导出、更新操作
* LDAP支持SSL (pem路径 jumpserver/data/certs/ldap_ca.pem)
* 支持Option方法请求API获取对应其他HTTP方法的所需的字段说明
* 支持RemoteApp

!!! summary "优化功能"

* 创建资产时允许ip字段填写为host地址
* OpenID Middleware去掉输出日志
* 资产节点API添加search功能
* 解决ldap映射is_active等字段为bool值的问题(可解决LDAP禁用用户后，同时禁止用户登录JumpServer的场景)

!!! success "修复Bug"

* 修复LDAP不能导入用户名中包含空格的用户
* 修复LDAP可导入跨页面选取的所有用户
* 修复资产用户管理器获取用户名为""的对象时返回多个结果的bug

1.4.10
------------------------
2019年4月30日

!!! note "新增功能"

* 新增权限控制：可分别对连接、上传、下载等动作单独授权；

!!! summary "优化功能"

* 权限优化：组织管理员不允许对超级管理员进行操作；
* Luna优化：Luna搜索优化功能；

!!! success "修复Bug"

* 修复通过API批量更新用户的bug
* 修复luna页面刷新不跳转OpeID认证的bug
* 修复创建azure类型的录像存储时前端的bug
* 修复其他前端页面bug
* 修复录像上传到Azure的bug

1.4.9
------------------------
2019年3月26日

!!! success "修复Bug"

* 修复创建定时任务时的时区问题
* 修复celery日志可能操作关闭文件的bug
* 修复一些设置缓存的问题
* 修复用户token过期的时间策略
* 修复第一次登录跳转组织页面的bug

!!! summary "优化功能"

* sudo命令添加帮助说明，并兼容换行形式
* 认证逻辑，从users模块中移动到authentication
* 合并一些migrations
* 任务列表去掉日期
* docker build升级Mysql client版本
* coco,guacamole上传完录像上报api, 页面上如果没有录像则播放按钮是禁用的
* 定时清理登陆日志
* 用户授权增加两层缓存，授权资产数量很大时也不怕了
* 资产模块添加资产用户管理器，可以为资产单独设置 管理用户、系统用户的密码
* 登陆日志的导出
* 数据库支持ssl
* ldap用户一键导入
* 使用网关同样添加心跳信息
* 用户授权资产列表增加缓存
* 修复一些sftp的小bug
* 修复上传命令记录decode的错误
* 支持系统用户在不同机器上密码不一致的场景
* 支持左侧列表缓存

1.4.8
------------------------
2019年2月22日

* 修复command filter 不记录操作日志的问题
* LDAP支持无密码
* 录像上传设置中去掉了ceph, s3兼容cepht
* gunicorn日志切割
* telnet支持在设置中修改成功的正则表达式
* 修复session 10分钟后不在线的问题

1.4.7
------------------------
2019年1月29日

* 支持 radius认证
* 统一生成coco的host key, 这样部署多个coco也不需要再复制 Host key
* 权限列表增加详细过滤
* 更改配置文件类型为 yml格式
* 修改心跳方式
* 优化任务执行的日志记录方式
* 修复节点右击测试连接资产为节点下所有资产, 而不是直接资产
* sftp支持修改home目录, 支持不显示隐藏文件
* 修复luna隐藏侧边栏的bug
* luna支持直接登录到某个资产

1.4.6
------------------------
2018年12月19日

* 推送资产上已存在的系统用户会覆盖该用户的home目录权限
* 会话日志可以定时清理, 保证硬盘够用
* coco里 p可以自定义是否分页了
* 优化树形结构, 不怕资产太多了
* 其他bug

1.4.5
------------------------
2018年12月12日

* 统一维护migrations数据库表结构变更
* 系统配置内容支持热加载, 不用再重启 jumpserver
* coco, guacamole注册机制更改, 使用预共享秘钥自动注册, 不再需要接受注册
* 用户密码过期时间设置
* ldap不可以修改密码
* 默认组织里可以看到所有用户
* 日志审计修改密码日志中只能看到当前组织用户的更改
* luna列表回滚为原来方式, 不再是异步加载
* rdp支持分辨率更改

1.4.4
------------------------
2018年11月11日

* 录像存储设置, 使用表单来填写
* 支持luna异步加载
* 各列表统一使用分页
* 授权时间精确到分钟
* 支持openid认证

1.4.3
------------------------
2018年10月12日

* 支持命令过滤

1.4.2
------------------------
2018年10月8日

* 支持web sftp, 支持跨资产复制粘贴文件
* 优化一些内容

1.4.1
------------------------
2018年9月4日

* 系统设置支持加密存储
* 单独推送系统用户到某个资产
* 支持了用户改密日志和操作日志
* 翻译更加完善, 支持切换语言
* 不记录zmodem信息
* 支持空闲间隔自动断开
* 修复session无法中断问题
* 增加ssh用户黑名单和白名单
* luna支持搜索支持IP
* 优化一些内容

1.4.0
------------------------
2018年8月7日

* 超级管理员创建组织, 为改组织添加管理员, 管理员可以负责该组织下 用户、资产、授权等管理
* Sftp显示同名资产为 主机名.组织
* Luna支持根据IP搜索
* 鼠标悬停可以显示主机ip
* 其他修复Bug等

1.3.3
------------------------
2018年7月17日

* 支持telnet协议
* 支持用户手动输入密码登陆, 密码不用托管到JumpServer
* 登陆日志增加失败原因
* session增加登陆源
* 修复网关端口和密码bug
* 添加用户登陆失败次数限制

1.3.2
------------------------
2018年6月11日

* 可以在系统设置中指定密码强度, 包含大小写字母特殊字符长度等
* 可以全局开启MFA
* 修改EMAIL不需要重启
* 设置公钥交互改变
* 修改一些BUG
* 修改窗口大小策略
* 统一requirements版本
* 修改luna树形结构, 从根开始展示
* 修改luna树形搜索
* 修改初始窗口大小不对的bug
* 修改录像播放的部分bug

1.3.1
------------------------
2018年5月24日

* 用户授权节点逻辑更改
* 去掉window无用信息
* 修复节点创建bug
* 创建节点 从0开始, 新节点0 新节点1
* 修复拖动节点引起的父节点异常
* 资产树增加视图, 只显示本节点资产和显示子节点资产

1.3.0
------------------------
2018年5月2日

* 支持二次认证(Google Authenticator)
* 修复一些bug
* 优化第一次登录页面

1.2.0
------------------------
2018年4月13日

* sftp上传文件支持
* 支持sftp日志审计

1.1.1
------------------------
2018年4月6日

* 加强任务执行
* 支持查看各个任务的详细执行日志
* 支持实时查看任务执行输出

1.1.0
------------------------
2018年4月3日

* 支持混合云多网络环境
* 网域概念加入
* 网关概念加入
* rdp gateway概念加入
* 修复一些bug

1.0.0
------------------------
2018年3月15日

* Windows支持
* 容器化部署
* 资产树
* 录像/命令存储支持OSS/S3和ES
* 分布式部署
* 系统用户自动推送
* 标签管理
* 命令统计增加输出展示
* Web Terminal改进
* 系统设置
* LDAP支持

0.5.0beta
------------------------
2017年5月21日

* coco和luna功能拆分
* 系统设置支持
* 录像支持
* 作业中心优化
* 其它修复Bug

0.4.0beta
---------------------------
2017年5月21日

* 使用最新版Python和Django开发  Python3.6.1, Django 1.11
* 使用完全使用 Django Class Base View开发
* 代码结构更加合理规整, 分组件开发
* 支持Restful API
* 拆分 JumpServer, terminal, web termial为三个项目 JumpServer, coco, luna。coco和luna为无状态的, 支持扩展
* 支持国际化, 英文+中文
* Ansible使用 2.1 版本
* 各组件功能都有所加强
* 支持登陆验证码
* 命令详细解析存储到数据库
* 登录记录审计
* 原来的手动推送用户改为自动推送
* 原来的connect脚本, 改为实现 ssh server, 统一了认证
* web terminal 无与伦比的漂亮
* 资产用户批量导入导出, 批量修改
* 界面更加优雅漂亮

0.3.3
------------------------
2016年12月14日

* 修改一些小bug

0.3.2
------------------------
2016年4月5日

* 模糊匹配支持
* 搜索排序问题
* 批量命令优化, ip获取

0.3.1
------------------------
2016年3月31日

* 优化ssh连接速度
* 优化web terminal窗口大小
* 修复录像播放白屏
* 优化命令匹配
* 优化安装脚本
* 优化Kill任务
* 修复监控卡住bug

0.3.0
------------------------
2015年12月20日

* 精确记录执行命令
* 新增文件上传下载
* 更改为输入ID登陆主机
* 增加主机搜索
* 执行命令使用ansible执行
* 优化脚本
* 增加web terminal
* 增加web端批量命令执行
* 增加录像回放
* 资产增加硬件信息抓取
* 资产增加Excel导出和导入
* 资产增加批量更改
* 在主机上授权系统用户(系统用户为一些通用用户, 如dev, dba等)
* 授权改为以授权规则为中心
* 添加系统用户推送
* 更改sudo管理
* 增加执行命令日志审计
* 增加文件上传命令审计
* 增加web端历史命令搜索

0.2.0
------------------------
2015年04月19日

* 使用paramiko原生ssh协议登录后端主机(原来版本使用pexpect模拟登录)
* 新增使用别名或备注登录
* 新增主机分组查看, 使用更方便
* 多线程批量执行命令
* 优化登录脚本
* Web界面更加美观漂亮
* 增加部门管理员负责管理本部门成员
* 增加仪表盘统计信息
* 增加部门, 用户组, 主机组
* 用户信息, 主机信息更加详细
* 主机登录方式增加登录方式 map, 用于登录不支持ldap的主机
* 主机授权, sudo授权改为组组之间授权
* 增加主机批量修改, 批量添加
* 添加用户自动生成随机密码, 然后自动发送邮件
* 添加各种搜索
* 增加普通用户web页面的授权申请
* 审计界面更加友好
* 主机添加过滤搜索功能
* 增加用户头像
* 上传批量上传
* 增加部门管理员页面
* 普通用户页面内容更加丰富

0.1.1
-----------------------
2014年11月14日

* 去掉shell脚本, 来添加用户
* 登录更稳定
* 新增Web控制sudo
* 新增Web查看统计日志
* 新增Web实时查看session屏幕
* 新增Web可以结束用户session
* 新增区分组管理员和超级管理员
* 新增web上传和下载文件
* 新增批量执行命令记录日志
* 新增上传下载记录日志
* 新增用户可以web修改密码
* 新增admin可以修改用户信息
* 新增IDC
* 支持分页
* admin可以下载用户key

0.1.0
----------------------
2014年8月15日

* 发布第一个版本
* bootstrap基本页面
* 用户管理
* 资产管理
* 授权资产给用户
* pexpect登录资产, 记录日志
* 服务器配置ldap, 集中认证
* 批量执行命令