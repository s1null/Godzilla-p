# 🔧 Profile功能使用说明
> 📌 本项目基于 [Godzilla](https://github.com/BeichenDream/Godzilla) , [Z-Godzilla_ekp](https://github.com/kong030813/Z-Godzilla_ekp) 构建
>

## 📖 1. 基本介绍
Profile功能用于自定义请求和响应模板，可以帮助你更好地控制WebShell的通信过程。它采用动态payload分割机制，通过随机分割和分布方式提高通信的隐蔽性。

## 🎬 效果展示
### 请求模板
```cpp
test1=##req-payload##&test2=##req-payload##&test3=##req-payload##&test4=##req-payload##&test5=##req-payload##&test6=##req-payload##
```

### 响应模板
```cpp
<title>##length##</title>
<!--payload1=##rep-payload##-->
<!--payload2=##rep-payload##-->
<!--payload3=##rep-payload##-->
<!--payload4=##rep-payload##-->
<!--payload5=##rep-payload##-->
<!--payload6=##rep-payload##-->
<!--payload7=##rep-payload##-->
<!--payload8=##rep-payload##-->
<!--payload9=##rep-payload##-->
```

### 状态码：404
### 效果图
![](https://cdn.nlark.com/yuque/0/2025/jpeg/26939533/1736340917757-2759f221-8d97-496c-8f56-bc4384ccfc3d.jpeg)

![](https://cdn.nlark.com/yuque/0/2025/jpeg/26939533/1736340921437-5185e193-c69e-4264-ba47-b7fdadd78e84.jpeg)

## ⚠️ 重要提示
使用Profile功能时，请注意：

1. 生成WebShell时必须选择带有`PROFILE`标识的加密器

如图所示：

    - 选择`JAVA_AES_BASE64_AVbypass_PROFILE`类型
    - 可以使用"生成文本"选项快速生成测试文件

![](https://cdn.nlark.com/yuque/0/2025/png/26939533/1736339895802-7976edac-e65b-40c8-8739-d327a3551d4b.png)  
![](images/generate_shell.png)

2. 连接WebShell时同样需要选择带有`PROFILE`标识的加密器

![](https://cdn.nlark.com/yuque/0/2025/png/26939533/1736339916403-0cf90686-258a-44ac-a975-90bb85461456.png)



3. 可以通过顶部菜单栏的"配置" -> "Profile配置"来管理Profile

![](https://cdn.nlark.com/yuque/0/2025/png/26939533/1736339795655-6f758967-5553-45af-8814-1e1227b0ebf6.png)

## 🔥 2. 核心特性
-🔄 动态Payload分割：每次请求都会随机分割payload

+ 🎯 灵活分布机制：将分割后的payload分布在profile模板的不同位置
+ 🛡️ 可变长度：避免了固定长度特征，提高隐蔽性
+ 🎭 模板匹配：支持自定义请求和响应模板

## ⭐ 3. 主要功能
Profile管理器分为两个主要标签页：

+ 📝 修改Profile：用于管理和编辑现有的Profile配置
+ 🆕 生成Profile：通过实际网页请求生成新的Profile配置

## 🎯 4. Profile配置项
每个Profile包含以下配置项：  
-📤 请求模板（Request Template）：定义请求数据的格式

+ 📥 响应模板（Response Template）：定义响应数据的格式
+ 🔢 状态码（Status Code）：自定义HTTP响应状态码
+ 📌 配置名称（Profile Name）：用于标识不同的Profile

## 🔐 5. 认证机制
### 5.1 基础认证
+ 🔑 使用密码（pass）和密钥（key）作为基本认证
+ 🛡️ 作为WebShell连接的第一层安全验证

### 5.2 Profile认证流程
1. 📤 首次连接：
    - 传递参数：`_profile`（base64编码）
    - 格式：`base64(pass|key|requestTemplate|responseTemplate|statusCode)`
2. 💾 Session处理：
    - WebShell接收并验证认证信息
    - 将模板信息保存在当前session中
3. 🔄 后续通信：
    - 使用profile中定义的参数格式
    - 按模板规则处理请求和响应

## 🚀 6. 使用方法
### 6.1 创建新Profile
#### 📋 方法一：手动创建（推荐）
1. ➡️ 点击Profile列表右键菜单中的"新建"
2. ➡️ 切换到"生成Profile"标签页
3. ➡️ 填写配置名称（Save Name）
4. ➡️ 编写请求模板和响应模板
5. ➡️ 设置状态码
6. ✅ 点击"保存"按钮

#### 🌐 方法二：通过URL生成（不推荐）
1. ➡️ 切换到"生成Profile"标签页
2. ➡️ 在Target URL中输入目标网址
3. ➡️ 点击"获取"按钮获取页面内容
4. ➡️ 填写配置名称（Save Name）
5. ➡️ 设置状态码
6. ✅ 点击"保存"按钮

### 6.2 管理Profile
在Profile列表中右键可以进行以下操作：

+ ✨ 新建：创建新的Profile
+ 🔄 刷新：更新Profile列表
+ 🗑️ 删除：移除选中的Profile
+ 📤 导出：将Profile配置导出到文件
+ 📥 导入：从文件导入Profile配置

### 6.3 编辑Profile
1. 👆 在左侧列表中选择要编辑的Profile
2. ✏️ 在右侧编辑区修改请求模板、响应模板或状态码
3. 💾 点击"保存"按钮保存修改

## 🔍 7. 模板语法
### 7.1 请求模板
+ 🔖 使用`##req-payload##`标记来指定payload在请求中的位置
+ ✅ 可以添加自定义参数和头部信息

### 7.2 响应模板
+ 🔖 使用`##rep-payload##`标记来指定payload在响应中的位置
+ 📏 使用`##length##`标记来指定分片长度信息

## ⚠️ 8. 已知问题和解决方案
### 8.1 导出问题
+ 🐛 问题：导出的profile文件中缺少状态码信息
+ 💡 解决方案：
    - 导入profile后手动设置状态码
    - 重新保存以更新配置

### 8.2 URL获取功能局限性
+ ⚠️ 问题：通过URL获取的profile可能不完整
+ 💡 建议：
    - 手动抓取目标网站的请求和响应
    - 自行构造profile模板
    - 不推荐使用自动URL获取功能

### 8.3 特殊字符处理
+ 🚫 问题：profile模板中包含分隔符"|"会导致解析失败
+ ⚠️ 影响：可能导致WebShell连接失败
+ 💡 解决方案：
    - 避免在模板中使用"|"字符
    - 需要使用时考虑其他替代字符
    - 使用前进行充分测试

## 🔍 9. 测试建议
### 9.1 Profile模板测试
+ ✅ 测试基本连接功能
+ ✅ 验证请求参数的正确传递
+ ✅ 确认响应模板的正确解析
+ ✅ 检查状态码是否正常返回

### 9.2 特殊情况测试
+ 📝 测试包含特殊字符的模板
+ 🔄 测试长数据传输
+ 🌐 测试不同编码的数据
+ 🔒 测试session保持性

## 💡 10. 最佳实践
### 10.1 Profile构建建议
```plain
✅ 推荐做法：
- 手动抓取目标网站流量
- 仔细分析请求和响应特征
- 构建符合目标特征的模板
- 避免使用特殊分隔字符

❌ 避免做法：
- 直接使用URL自动获取
- 使用未经测试的特殊字符
- 构建过于复杂的模板
```

### 10.2 测试流程
1. 🔍 先测试基本连接
2. 📝 测试模板解析
3. 🔄 测试数据传输
4. ⚠️ 测试异常情况
5. 📊 验证状态码

### 10.3 故障排查
当连接失败时，按以下步骤排查：

1. ✅ 检查基本认证信息（pass和key）
2. 📝 检查profile模板中是否包含特殊字符
3. 🔍 验证base64编码是否正确
4. 📦 确认session是否正常保持
5. 🔢 验证状态码设置

## ⚠️ 11. 注意事项
+ ❌ Profile名称不能重复  
-📝 导入Profile时需要指定新的配置名称
+ 💾 修改Profile后需要点击保存才能生效
+ ⚠️ 删除操作不可恢复，请谨慎操作

> 🌟 小贴士：这样的Profile功能可以帮助你更好地伪装WebShell流量，提高隐蔽性和稳定性。通过自定义请求和响应模板，可以使WebShell通信更接近正常网站的行为特征。
>

## 🆕 小细节修改
1. ✨ 新增功能：
    - 📝 生成Shell界面新增"生成文本"选项
    - 🎯 点击后将直接在桌面生成`config.txt`文件
    - 💡 便于快速测试和调试Shell
2. 🎨 界面优化：
    - 📊 优化了主界面右侧分组栏的默认宽度
    - 🔧 无需每次手动调整宽度
    - 👀 提供更好的视觉体验



## ⚖️ 免责声明
### 使用须知
1. 本工具仅供安全研究和授权测试使用
2. 使用本工具进行测试时需获得测试目标的授权
3. 禁止对未授权的目标进行测试

### 责任声明
1. 使用者应对自己的行为负全部责任
2. 开发者不对任何人以任何方式使用本工具所造成的任何直接或间接损失负责
3. 如果您遇到因使用本工具造成的任何问题，请立即停止使用

### 法律信息
1. 本工具仅可用于：
    - 授权的渗透测试
    - 安全研究和学习
    - 网络安全教育
2. 禁止用于：
    - 未经授权的入侵测试
    - 任何非法用途
    - 对他人进行攻击

### 使用条款
1. 使用本工具即表示您同意：
    - 完全了解并接受上述免责声明
    - 承诺遵守相关法律法规
    - 承担使用过程中的所有风险
2. 如果您不同意这些条款，请勿使用本工具

> ⚠️ 警告：违反上述声明造成的任何问题，均与本工具作者及维护者无关
>

---

