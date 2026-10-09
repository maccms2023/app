# 🚀 快速 APK 打包指南

## ⚡ 最快方式（5分钟内完成）

### 第一步：下载并解压
```bash
# 1. 从 GitHub 下载 ZIP
wget https://github.com/maccms2023/app/blob/main/android-tv-project.zip

# 或在浏览器中下载，然后解压
unzip android-tv-project.zip
cd android-tv-project
```

### 第二步：构建 APK（调试版 - 推荐新手）
```bash
./gradlew assembleDebug
```

**等待 2-5 分钟...** ✅

### 第三步：获取 APK 文件
```
生成位置：app/build/outputs/apk/debug/app-debug.apk
```

**直接使用这个 APK 文件安装到设备即可！**

---

## 📦 三种 APK 打包方案

| 方案 | 大小 | 速度 | 用途 | 命令 |
|------|------|------|------|------|
| **调试版** | 小 | 快 ⚡ | 开发测试 | `./gradlew assembleDebug` |
| **发布版** | 中 | 中 | Google Play | `./gradlew assembleRelease` |
| **优化版** | 最小 | 快 | 生产环境 | `./gradlew bundleRelease` |

---

## 📥 一行命令打包（适合 CI/CD）

```bash
# 进入项目目录后执行
./gradlew assembleDebug -q && \
echo "✅ APK 已生成：app/build/outputs/apk/debug/app-debug.apk"
```

---

## 🎯 完整步骤（Windows 用户）

```cmd
REM 1. 解压（假设已下载 ZIP）
powershell -Command "Expand-Archive -Path 'android-tv-project.zip' -DestinationPath '.'"

REM 2. 进入项目
cd android-tv-project

REM 3. 构建 APK
gradlew.bat assembleDebug

REM 4. 查看输出
echo APK 位置：app\build\outputs\apk\debug\app-debug.apk
```

---

## 📱 构建完成后

| 文件 | 位置 | 大小 | 安装方式 |
|------|------|------|--------|
| app-debug.apk | `app/build/outputs/apk/debug/` | ~30-50MB | ADB 或直接安装 |

### 安装到设备
```bash
# 连接设备后执行
adb install app/build/outputs/apk/debug/app-debug.apk

# 或直接传输到设备手动安装
adb push app/build/outputs/apk/debug/app-debug.apk /sdcard/
```

---

## ✅ 前置要求检查清单

- [ ] JDK 11+ 已安装：`java -version`
- [ ] Android SDK 已安装：设置 `ANDROID_HOME` 环境变量
- [ ] 网络连接正常（首次会下载 Gradle 依赖 ~500MB）
- [ ] 磁盘空间充足（至少 2GB）

---

## 🔥 常见错误快速修复

### ❌ "找不到 gradlew"
```bash
chmod +x gradlew  # Linux/macOS
```

### ❌ "ANDROID_HOME 未设置"
**Windows:**
```
设置环境变量：ANDROID_HOME = C:\Users\YourName\AppData\Local\Android\Sdk
```

**Linux/macOS:**
```bash
export ANDROID_HOME=~/Android/Sdk
```

### ❌ "Java 版本不兼容"
```bash
# 安装 JDK 11+
# 或指定 JAVA_HOME
export JAVA_HOME=/path/to/jdk11
```

### ❌ "Gradle 下载超时"
```bash
# 清除缓存重试
./gradlew clean --refresh-dependencies assembleDebug
```

---

## 📊 构建时间参考

- 首次构建：3-10 分钟（需下载依赖）
- 后续构建：1-3 分钟（有缓存）
- 完全清理重建：5-15 分钟

---

## 💡 性能优化

### 加速构建
```bash
export GRADLE_OPTS="-Xmx2048m"
./gradlew assembleDebug --daemon --parallel
```

### 后台守护进程
```bash
./gradlew --daemon assembleDebug
```

停止守护进程：
```bash
./gradlew --stop
```

---

## 📝 输出示例

```
> Task :app:assembleDebug

BUILD SUCCESSFUL in 2m 15s
34 actionable tasks: 34 executed

✅ APK 文件已生成！
📍 位置：app/build/outputs/apk/debug/app-debug.apk
📦 大小：42.5 MB
```

---

## 🎁 额外命令

```bash
# 只编译不打包
./gradlew compileDebug

# 查看所有可用任务
./gradlew tasks

# 查看构建详细信息
./gradlew assembleDebug -i

# 跳过测试加速构建
./gradlew assembleDebug -x test
```

---

## 📞 需要发布版？

如需上架应用商店，使用发布版本：

```bash
./gradlew assembleRelease
```

需要配置签名密钥文件（`.jks`），详见完整文档。

---

**现在就开始：** `./gradlew assembleDebug` ⚡

