# 菜鸟裹裹 Loon 去广告插件

基于菜鸟裹裹 iOS 抓包中出现的第三方广告 SDK 请求，屏蔽穿山甲、1RTB、Ubixioe 和腾讯优量汇相关广告域名。规则只针对抓包中辨识出的广告服务域名，不拦截菜鸟物流接口。

## 安装

在 Loon 中添加插件：

```text
https://raw.githubusercontent.com/loiiw/cnads/main/cainiao-adblock.plugin
```

## 规则范围

| 域名 | 抓包中的用途线索 |
| --- | --- |
| `api-access.pangolin-sdk-toutiao-b.com` | 穿山甲广告请求（`/api/ad/union/sdk/get_ads/`） |
| `sdk.1rtb.net` | 广告请求（`/sdk/req_ad`） |
| `entry-su1.ubixioe.com` | 广告 SDK 请求（`/mob/sdk/v2/endpoint`） |
| `adx-cfg-u1.ubixioe.com` | Ubixioe 广告 SDK 初始化配置 |
| `win.gdt.qq.com` | 腾讯广告 SDK 请求（`/win_notice.fcg`） |

插件使用 Loon 的域名拒绝规则，不需要 MitM 证书。

## 说明

当前抓包证明这些 SDK 请求在该次会话中出现过，但不足以确认菜鸟所有页面的广告来源。由菜鸟自有接口返回或直接嵌入页面内容的广告不在此规则范围内；如果仍有广告，请提供广告出现页面附近的新抓包，以便补充精确规则。
