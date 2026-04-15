# AGENTS.md

- 单模块 Maven 项目，代码在 `src/main/java/com/hankcs/lucene`，测试在 `src/test/java/com/hankcs/lucene`。
- 常用验证命令：`mvn test`；打包命令：`mvn package`（产物在 `target/hanlp-lucene-plugin-*.jar`）。
- 只跑单测请用 Surefire 过滤：`mvn -Dtest=HanLPAnalyzerTest test` 或 `mvn -Dtest=HanLPAnalyzerTest#testIssue test`。
- 本地不要默认跑 `mvn verify`：`pom.xml` 绑定了 `maven-gpg-plugin` 到 `verify` 阶段，缺少签名环境会失败。
- 语言级别固定为 Java 7（`javac.src.version/javac.target.version=1.7`）；JDK 8+ 下通过 `disable-java8-doclint` profile 关闭了 javadoc doclint。
- `enableIndexMode=true` 仅应用于索引阶段 analyzer；查询阶段不要开启（README 已明确说明）。
- `HanLPTokenizerFactory` 会改写 HanLP 全局配置（`HanLP.Config.Normalization`、`HanLP.Config.CustomDictionaryPath`、`HanLP.Config.enableDebug()`），测试之间可能互相污染。
- `enableTraditionalChineseMode` 分支会写入 `TraditionalChineseTokenizer.SEGMENT`（静态字段），这是另一处全局状态，改动分词行为时优先关注。
- 仓库内无 CI/workflow 或额外任务编排配置；构建与发布行为以 `pom.xml` 为准，README 仅作补充。
