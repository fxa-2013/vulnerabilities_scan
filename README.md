# 梦鉴 - 网络安全评估系统
<img width="1894" height="908" alt="image" src="https://github.com/user-attachments/assets/4fa2caae-9b76-4790-ab91-8fba2d0e1233" />

## 项目简介

梦鉴是一款功能全面的网络安全评估系统，旨在帮助安全专业人员快速发现和评估网络中的安全隐患。系统采用前后端分离架构，前端使用HTML5、CSS3和JavaScript构建，后端使用Python Flask框架开发。
<img width="1920" height="920" alt="image" src="https://github.com/user-attachments/assets/64c4f563-91ae-44eb-840a-130d6372f640" />


## 系统架构

### 技术栈

- **前端**：HTML5, CSS3, JavaScript, Tabler UI框架
- **后端**：Python 3.9+, Flask 2.0+
- **数据库**：SQLite/MySQL
- **Web服务器**：Nginx (前端代理), Flask内置服务器 (后端API)
- **网络工具**：curl、telnet、ip等

### 部署架构

```
┌───────────────────────────────────────────────────────────┐
│                         用户浏览器                        │
└───────────────────────┬───────────────────────────────────┘
                        │
┌───────────────────────▼───────────────────────────────────┐
│                      Nginx (8080)                        │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐  │
│  │                  前端静态文件                      │  │
│  │  (HTML, CSS, JavaScript, 图片等)                   │  │
│  └─────────────────────────────────────────────────────┘  │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐  │
│  │            API请求反向代理 (/api/)                │  │
│  └──────────────────────────────┬──────────────────────┘  │
└─────────────────────────────────┼─────────────────────────┘
                                  │
┌─────────────────────────────────▼─────────────────────────┐
│                     Flask后端 (5000)                     │
│                                                           │
│  ┌─────────────────────────────────────────────────────┐  │
│  │                    API路由处理                     │  │
│  ├─────────────────────────────────────────────────────┤  │
│  │                  业务逻辑处理                      │  │
│  ├─────────────────────────────────────────────────────┤  │
│  │                 数据库操作                         │  │
│  ├─────────────────────────────────────────────────────┤  │
│  │                网络工具调用                        │  │
│  └─────────────────────────────────────────────────────┘  │
└───────────────────────────────────────────────────────────┘
```
### 部署资源
推荐4核8G内存100G存储使用！
## 功能模块详解

### 1. 系统首页 (index.html)

**核心功能**：系统概览、资源监控、任务统计

**实现方式**：
- 使用Tabler UI框架构建响应式布局
- 通过AJAX请求后端API获取实时数据
- 使用ApexCharts绘制系统资源使用图表
- 显示系统运行状态、任务统计和资源利用率

**关键API**：
- `/api/system/stats` - 获取系统状态信息
- `/api/monitoring/stats` - 获取监控数据
- `/api/tasks` - 获取任务统计信息

### 2. 资产管理 (asset-management.html)
<img width="1919" height="911" alt="image" src="https://github.com/user-attachments/assets/8c6fd8f1-140f-4335-9f78-fa1f19a798d4" />

**核心功能**：资产分组管理、资产信息管理

**实现方式**：
- 左侧资产分组树状结构
- 右侧资产列表表格，支持分页和搜索
- 模态框形式的资产添加/编辑界面
- 支持资产状态监控和分类管理

**关键API**：
- `/api/assets` - 资产列表和管理
- `/api/asset-groups` - 资产分组管理

### 3. 主机探测 (host-detection.html)

**核心功能**：网络主机存活探测
<img width="1321" height="848" alt="image" src="https://github.com/user-attachments/assets/99ae3ca8-ff1c-4c62-8389-311b66c7dd33" />

**实现方式**：
- 支持多种探测方式（ICMP、TCP SYN、ARP等）
- 可配置探测参数（超时时间、并发数等）
- 实时显示探测进度和结果
- 支持探测结果导出

**关键API**：
- `/api/host-discovery/start` - 启动主机探测任务
- `/api/host-discovery/status` - 获取探测状态
- `/api/host-discovery/results` - 获取探测结果

### 4. 端口检测 (port-detection.html)
<img width="1474" height="888" alt="image" src="https://github.com/user-attachments/assets/b810367e-f560-4415-a48a-55929d69fa92" />

**核心功能**：端口扫描和服务识别

**实现方式**：
- 支持多种扫描模式（全端口、常用端口、自定义端口）
- 可配置扫描速度和深度
- 实时显示扫描进度和开放端口信息
- 支持服务识别和版本检测

**关键API**：
- `/api/port-scan/start` - 启动端口扫描任务
- `/api/port-scan/status` - 获取扫描状态
- `/api/port-scan/results` - 获取扫描结果

### 5. 服务指纹 (service-fingerprint.html)
<img width="1433" height="905" alt="image" src="https://github.com/user-attachments/assets/22d3c7bd-1f3e-4b21-ac32-d79fdbc247a5" />

**核心功能**：服务识别和版本检测

**实现方式**：
- 基于特征匹配的服务识别
- 支持常见服务的版本检测
- 可自定义服务指纹规则
- 支持批量服务识别

**关键API**：
- `/api/service-fingerprint/scan` - 启动服务识别任务
- `/api/service-fingerprint/results` - 获取识别结果
- `/api/service-fingerprint/rules` - 管理服务指纹规则

### 6. 弱密码检测 (weak-password.html)
<img width="1884" height="906" alt="image" src="https://github.com/user-attachments/assets/ddaf5406-5f7a-4ea4-b420-b1acfc0ae374" />

**核心功能**：弱密码扫描和检测

**实现方式**：
- 支持多种协议的弱密码检测（SSH、FTP、SMB等）
- 内置弱密码字典
- 可配置扫描参数和字典
- 实时显示扫描进度和结果

**关键API**：
- `/api/weak-password/scan` - 启动弱密码扫描任务
- `/api/weak-password/status` - 获取扫描状态
- `/api/weak-password/results` - 获取扫描结果

### 7. 操作系统扫描 (os_scan.html)
<img width="1920" height="920" alt="image" src="https://github.com/user-attachments/assets/e3b51596-be57-4386-a03c-27bf672ecc6a" />

**核心功能**：操作系统类型和版本识别

**实现方式**：
- 基于TCP/IP栈指纹的操作系统识别
- 支持多种扫描技术
- 可配置扫描深度和准确度
- 实时显示识别结果

**关键API**：
- `/api/os-detection/scan` - 启动操作系统识别任务
- `/api/os-detection/results` - 获取识别结果
- `/api/os-detection/fingerprints` - 管理操作系统指纹规则

### 8. 漏洞扫描 (vulnerability-scan.html)
<img width="1885" height="909" alt="image" src="https://github.com/user-attachments/assets/198bf62e-70ab-4627-a838-d6d59b8588be" />

**核心功能**：漏洞检测和评估

**实现方式**：
- 基于POC的漏洞检测
- 支持多种漏洞类型
- 可配置扫描策略和深度
- 实时显示扫描进度和漏洞信息
- 提供漏洞风险评估和修复建议

**关键API**：
- `/api/vulnerability/scan` - 启动漏洞扫描任务
- `/api/vulnerability/status` - 获取扫描状态
- `/api/vulnerability/results` - 获取扫描结果
- `/api/vulnerability/pocs` - 管理漏洞POC库

### 9. 网络管理 (network-management.html)
<img width="1920" height="884" alt="image" src="https://github.com/user-attachments/assets/b866e21a-5d1e-4ca6-b164-81b7fd49d6fd" />

**核心功能**：网络接口、路由和DNS管理

**实现方式**：
- 标签页形式的网络管理界面
- 物理接口信息展示和管理
- 路由表查看和管理
- DNS客户端配置管理

**关键API**：
- `/api/network/interfaces` - 获取网络接口信息
- `/api/network/routes` - 获取路由表信息
- `/api/network/dns` - 获取DNS配置信息

### 10. 任务管理
<img width="1312" height="902" alt="image" src="https://github.com/user-attachments/assets/cb9f5f46-0f31-4098-9bcc-9b9f2425dbdf" />
<img width="1324" height="913" alt="image" src="https://github.com/user-attachments/assets/28ce5240-e01c-408e-898b-6764ffdee347" />


#### 任务列表 (task-list.html)
<img width="1310" height="199" alt="image" src="https://github.com/user-attachments/assets/9630fab9-a1ec-4011-bab5-c2633ac7fd02" />

**核心功能**：任务状态查看和管理

**实现方式**：
- 任务列表表格，支持分页和搜索
- 实时显示任务状态和进度
- 支持任务暂停、取消和删除
- 提供任务结果查看和导出

**关键API**：
- `/api/tasks` - 获取任务列表
- `/api/tasks/{id}` - 获取任务详情
- `/api/tasks/{id}/cancel` - 取消任务

#### 任务创建 (task-create.html)

**核心功能**：创建新的扫描任务

**实现方式**：
- 向导式任务创建界面
- 支持多种任务类型配置
- 可设置任务调度和通知
- 提供任务模板和批量创建

**关键API**：
- `/api/tasks/create` - 创建新任务
- `/api/task-templates` - 获取任务模板

### 11. 系统维护 (system-maintenance.html)
<img width="1331" height="347" alt="image" src="https://github.com/user-attachments/assets/0c13810e-17ac-42e6-a130-e9864c091345" />
<img width="1302" height="576" alt="image" src="https://github.com/user-attachments/assets/9086e918-43bc-4fc1-9ce5-dd0ef27e0843" />

**核心功能**：系统配置和维护

**实现方式**：
- 系统服务管理
- 磁盘和内存管理
- 系统更新和备份
- 系统日志查看
<img width="1908" height="914" alt="image" src="https://github.com/user-attachments/assets/19e85bee-d226-4ba5-989e-9fe51a775cae" />

**关键API**：
- `/api/system/services` - 管理系统服务
- `/api/system/maintenance` - 系统维护操作
- `/api/system/backup` - 系统备份和恢复

### 12. 用户管理 (user-management.html)
<img width="1323" height="410" alt="image" src="https://github.com/user-attachments/assets/f74b6bcf-6098-4518-bf37-f45c7cbd1227" />
<img width="1382" height="912" alt="image" src="https://github.com/user-attachments/assets/45e7ae13-6edc-4f19-b450-f36c66f08abe" />

**核心功能**：用户和权限管理

**实现方式**：
- 用户列表管理
- 角色和权限配置
- 用户登录和认证管理
- 操作审计日志
<img width="1902" height="916" alt="image" src="https://github.com/user-attachments/assets/cd8d163d-ab9a-43b2-8db4-855bef5c8adc" />

**关键API**：
- `/api/users` - 用户管理
- `/api/roles` - 角色管理
- `/api/permissions` - 权限管理

### 13. 日志中心 (log-center.html)
<img width="1433" height="877" alt="image" src="https://github.com/user-attachments/assets/25e1f25a-374b-4ecc-ac61-79a5db470601" />

**核心功能**：系统日志管理和分析

**实现方式**：
- 多类型日志查看（系统、安全、应用等）
- 日志搜索和过滤
- 日志分析和统计
- 日志导出和归档

**关键API**：
- `/api/logs` - 获取系统日志
- `/api/logs/search` - 搜索日志
- `/api/logs/export` - 导出日志

### 14. 基本设置 (basic-settings.html)
<img width="1280" height="783" alt="image" src="https://github.com/user-attachments/assets/9163628c-3fb6-43e1-9a39-fa5e9025c512" />

**核心功能**：系统基本配置

**实现方式**：
- 系统参数配置
- 网络设置
- 安全设置
- 通知配置

**关键API**：
- `/api/settings` - 获取和更新系统设置
- `/api/settings/network` - 网络设置
- `/api/settings/security` - 安全设置

### 15. 规则更新 (rule-update.html)
<img width="1423" height="902" alt="image" src="https://github.com/user-attachments/assets/9d9720bb-05ee-4662-9ba3-b60fe317bcd7" />

**核心功能**：安全规则更新和管理

**实现方式**：
- 规则库版本管理
- 规则更新和同步
- 自定义规则添加和管理
- 规则有效性检测

**关键API**：
- `/api/rules` - 规则管理
- `/api/rules/update` - 更新规则库
- `/api/rules/validate` - 验证规则有效性

### 16. 数据库管理

#### 弱密码数据库 (weak-password-db.html)
<img width="1335" height="704" alt="image" src="https://github.com/user-attachments/assets/9a021aea-6cdf-4751-84b9-2abda7960449" />

**核心功能**：弱密码字典管理

**实现方式**：
- 弱密码列表管理
- 密码强度评估规则
- 字典导入和导出
- 密码统计分析

**关键API**：
- `/api/weak-password/db` - 弱密码数据库管理
- `/api/weak-password/db/import` - 导入弱密码字典
- `/api/weak-password/db/export` - 导出弱密码字典

#### 操作系统指纹数据库 (os-fingerprint-db.html)
<img width="1310" height="755" alt="image" src="https://github.com/user-attachments/assets/d2677c82-3c55-44ae-841a-c236cce4805b" />

**核心功能**：操作系统指纹规则管理

**实现方式**：
- 操作系统指纹规则列表
- 规则添加、编辑和删除
- 规则测试和验证
- 规则导入和导出

**关键API**：
- `/api/os-fingerprints` - 操作系统指纹管理
- `/api/os-fingerprints/import` - 导入指纹规则
- `/api/os-fingerprints/export` - 导出指纹规则

#### 服务指纹数据库 (service-fingerprint-db.html)
<img width="1317" height="735" alt="image" src="https://github.com/user-attachments/assets/9bfa27d8-3337-49a5-bdbe-01089b902565" />

**核心功能**：服务指纹规则管理

**实现方式**：
- 服务指纹规则列表
- 规则添加、编辑和删除
- 规则测试和验证
- 规则导入和导出

**关键API**：
- `/api/service-fingerprints` - 服务指纹管理
- `/api/service-fingerprints/import` - 导入指纹规则
- `/api/service-fingerprints/export` - 导出指纹规则

#### 漏洞POC数据库 (vulnerability-poc.html)

**核心功能**：漏洞POC管理
<img width="1306" height="682" alt="image" src="https://github.com/user-attachments/assets/bafff563-c287-41ce-ba47-063faa6f13fc" />

**实现方式**：
- 漏洞POC列表管理
- POC添加、编辑和删除
- POC测试和验证
- POC导入和导出

**关键API**：
- `/api/vulnerability/pocs` - 漏洞POC管理
- `/api/vulnerability/pocs/import` - 导入POC
- `/api/vulnerability/pocs/export` - 导出POC

### 17. 端口映射 (port-mapping.html)
<img width="1315" height="711" alt="image" src="https://github.com/user-attachments/assets/df7ead76-a3ae-4251-a4f2-c0c70e87b284" />

**核心功能**：端口映射管理

**实现方式**：
- 端口映射规则列表
- 规则添加、编辑和删除
- 规则启用和禁用
- 规则测试和验证

**关键API**：
- `/api/port-mapping` - 端口映射管理
- `/api/port-mapping/test` - 测试端口映射

### 18. 其他功能

#### 游戏 (game.html)

**核心功能**：安全知识小游戏

**实现方式**：
- 安全知识问答游戏
- 积分和排行榜系统
- 游戏记录和统计

**关键API**：
- `/api/game/questions` - 获取游戏题目
- `/api/game/score` - 提交游戏分数
- `/api/game/rankings` - 获取排行榜

#### 登录系统 (sign.html)

**核心功能**：用户登录和认证

**实现方式**：
- 用户名密码登录
- 验证码安全保护
- 登录失败锁定
- 登录审计日志

**关键API**：
- `/api/auth/login` - 用户登录
- `/api/auth/logout` - 用户登出
- `/api/auth/refresh` - 刷新认证令牌

## 前端实现技术

### 1. 页面结构

- **响应式布局**：使用Bootstrap网格系统和Tabler UI框架
- **组件化设计**：导航栏、侧边栏、卡片、表格等可复用组件
- **模块化组织**：按功能模块划分HTML文件
- **统一导航**：使用navbar.html和footer.html实现全局导航和页脚

### 2. 数据交互

- **AJAX请求**：使用Fetch API进行后端API调用
- **实时数据**：通过定时轮询获取实时数据
- **WebSocket**：部分功能使用WebSocket实现实时通信
- **数据可视化**：使用ApexCharts绘制各种图表

### 3. 用户体验

- **表单验证**：前端表单验证和错误提示
- **加载状态**：操作过程中的加载动画
- **进度显示**：任务执行进度实时显示
- **结果反馈**：操作结果的视觉反馈
- **响应式设计**：适配不同屏幕尺寸

### 4. 安全性

- **CSRF保护**：前端CSRF令牌验证
- **输入验证**：所有用户输入的前端验证
- **安全头部**：适当的安全HTTP头部设置
- **密码加密**：密码强度检测和加密传输

## 后端实现技术

### 1. API设计

- **RESTful API**：遵循RESTful设计规范
- **资源路由**：按资源类型组织API路由
- **参数验证**：所有API参数的服务器端验证
- **错误处理**：统一的错误处理和响应格式

### 2. 核心功能

- **任务调度**：异步任务调度和管理
- **网络工具集成**：集成nmap、masscan等网络工具
- **指纹识别**：基于特征的服务和操作系统识别
- **漏洞检测**：基于POC的漏洞扫描
- **数据管理**：安全相关数据库的管理和更新

### 3. 安全特性

- **认证授权**：基于JWT的认证和基于角色的授权
- **访问控制**：细粒度的访问控制策略
- **审计日志**：详细的操作审计日志
- **安全扫描**：系统自身的安全扫描和评估

### 4. 性能优化

- **异步处理**：CPU密集型任务的异步处理
- **缓存机制**：频繁访问数据的缓存
- **并发控制**：合理的并发请求控制
- **资源管理**：系统资源的有效管理和监控

## 部署指南

### 环境要求

- **操作系统**：Linux (CentOS 8+, Ubuntu 18.04+)
- **Python**：3.9+
- **数据库**：SQLite 3.8+ 或 MySQL 5.7+
- **Web服务器**：Nginx 1.18+
- **网络工具**：N/A

### 部署步骤

1. **安装依赖**

   ```bash
   # 安装系统依赖
   sudo yum install -y epel-release
   sudo yum install -y python3 python3-pip nginx nmap masscan
   
   # 安装Python依赖
   cd /mj_scan/backend
   pip3 install -r requirements.txt
   ```

2. **配置Nginx**

   ```bash
   # 创建Nginx配置
   sudo vi /etc/nginx/conf.d/mj_scan.conf
   ```

   配置内容：

   ```nginx
   server {
       listen 8080;
       server_name localhost;
       
       root /mj_scan/frontend;
       index index.html;
       
       location / {
           try_files $uri $uri/ /index.html;
       }
       
       location /api/ {
           proxy_pass http://localhost:5000/api/;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
           proxy_set_header X-Forwarded-Proto $scheme;
       }
   }
   ```

3. **启动服务**

   ```bash
   # 启动后端服务
   cd /mj_scan/backend
   python3 app.py &
   
   # 启动Nginx服务
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

4. **设置开机自启动**

   ```bash
   # 使用start_all.sh脚本
   sudo cp /mj_scan/start_all.sh /etc/init.d/
   sudo chmod +x /etc/init.d/start_all.sh
   sudo update-rc.d start_all.sh defaults
   ```

### 访问方式

- **前端界面**：http://localhost:8080
- **后端API**：http://localhost:5000/api
- **默认登录**：admin / password

## 安全加固

### 1. 系统安全

- **GRUB密码保护**：设置GRUB启动密码，防止未授权修改启动参数
- **禁用单用户模式**：从GRUB菜单中移除单用户模式选项
- **文件系统权限**：严格的文件系统权限设置
- **服务最小化**：仅运行必要的系统服务

### 2. 应用安全

- **密码策略**：强密码要求和定期更换
- **访问控制**：基于角色的细粒度访问控制
- **API保护**：API请求频率限制和授权验证
- **输入验证**：所有用户输入的严格验证

### 3. 数据安全

- **数据加密**：敏感数据的加密存储
- **备份策略**：定期数据备份和恢复测试
- **审计日志**：详细的操作审计和安全事件日志
- **数据脱敏**：展示数据时的敏感信息脱敏

## 维护指南

### 1. 日常维护

- **系统更新**：定期更新系统和依赖包
- **规则更新**：定期更新安全规则和指纹库
- **日志清理**：定期清理和归档系统日志
- **性能监控**：监控系统资源使用情况

### 2. 故障排查

- **日志分析**：系统日志和应用日志分析
- **网络诊断**：网络连接和服务状态检查
- **性能分析**：系统性能瓶颈分析
- **数据库维护**：数据库优化和修复

### 3. 升级指南

- **备份数据**：升级前完整备份系统数据
- **测试环境**：在测试环境验证升级
- **分步升级**：分步骤进行系统组件升级
- **回滚计划**：制定详细的升级回滚计划

## 开发指南

### 1. 前端开发

- **开发环境**：推荐使用VS Code和Live Server
- **代码规范**：遵循HTML5、CSS3和JavaScript最佳实践
- **调试工具**：使用浏览器开发者工具进行调试
- **版本控制**：使用Git进行代码版本管理

### 2. 后端开发

- **开发环境**：推荐使用PyCharm或VS Code
- **代码规范**：遵循PEP 8 Python代码规范
- **调试工具**：使用Python调试器和日志系统
- **测试**：编写单元测试和集成测试

### 3. API开发

- **API文档**：使用Swagger或Postman生成API文档
- **版本控制**：API版本管理和向后兼容
- **性能测试**：API性能测试和优化
- **安全测试**：API安全测试和漏洞扫描

## 常见问题

### 1. 前端无法访问后端API

**问题**：前端显示API请求404错误
**解决方案**：
- 检查Nginx配置是否正确
- 确认后端服务是否运行
- 验证API路径是否正确
- 检查防火墙设置

### 2. 扫描任务无法启动

**问题**：点击扫描按钮后无响应
**解决方案**：
- 检查网络连接是否正常
- 确认后端服务是否有足够权限
- 验证扫描参数是否正确
- 查看系统日志中的错误信息

### 3. 系统资源占用过高

**问题**：系统CPU或内存使用过高
**解决方案**：
- 检查是否有长时间运行的扫描任务
- 调整扫描任务的并发数和速度
- 优化系统资源限制
- 考虑增加硬件资源

### 4. 数据库连接失败

**问题**：系统无法连接到数据库
**解决方案**：
- 检查数据库服务是否运行
- 验证数据库连接参数是否正确
- 确认数据库用户权限
- 检查数据库文件权限

## 许可证

本项目采用授权许可证，详情请参阅LICENSE文件。

## 免责声明

本系统仅用于合法的网络安全评估和教育目的，严禁用于任何未经授权的网络活动。使用本系统进行的任何操作所产生的法律责任由使用者自行承担。

## 联系方式

- **微信公众号：服安科技
- **技术支持**：联系客服

---

**版本**：v1.0.0
**发布日期**：2026-02-06
**开发团队**：梦鉴 - 安全团队
