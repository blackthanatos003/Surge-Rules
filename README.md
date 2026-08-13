# Surge Rules

## Surge Mac 6.8+ 模块用法

Surge 新版模块的 `[Rule]` 只能使用内置策略。模块不能直接引用主配置中的 `Proxy`、`PROXY` 等自定义策略组。为保留按需启停功能，本仓库的两个模块改用内联 Ruleset 桥接方案。

### A：主配置策略组名为 `Proxy`

在主配置中一次性加入：

```ini
[Ruleset RuleInjectorProxy]
DOMAIN,rule-injector-disabled.invalid

[Rule]
RULE-SET,RuleInjectorProxy,Proxy
```

然后安装并按需启用：

```text
https://raw.githubusercontent.com/acherontia003/Surge-Rules/main/A_inject-rules-proxy.sgmodule
```

### B：主配置策略组名为 `PROXY`

在主配置中一次性加入：

```ini
[Ruleset RuleInjectorPROXY]
DOMAIN,rule-injector-disabled.invalid

[Rule]
RULE-SET,RuleInjectorPROXY,PROXY
```

然后安装并按需启用：

```text
https://raw.githubusercontent.com/acherontia003/Surge-Rules/main/B_inject-rules-PROXY.sgmodule
```

占位域名使用 RFC 保留的 `.invalid` 顶级域，模块关闭时不会匹配正常流量。模块启用后，Surge 会把模块中的规则补入同名内联 Ruleset。

UURemote 使用 Surge Mac 6.0+ 的 App Bundle 匹配模式：

```ini
PROCESS-NAME,/Applications/UURemote.app/,DIRECT
```

该写法同时覆盖 `UURemote`、`UURemoteService` 和 `UURemoteDaemon`。
