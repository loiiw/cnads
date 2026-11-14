# 菜鸟裹裹 Loon 去广告插件

基于菜鸟裹裹 iOS 抓包中出现的第三方广告 SDK 请求和物流详情接口中的广告参数，屏蔽穿山甲、1RTB、Ubixioe 和腾讯优量汇相关广告，并从物流详情响应中删除广告查询参数。

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
| `cn-lde-mtop.cainiao.com` | 物流详情响应中移除 `data.globalData.formerModel.extPackageAttr.ADS_QUERY_PARAM` |

第三方广告域名使用 Loon 的域名拒绝规则。物流详情响应改写需要在 Loon 中启用 HTTPS 解密并信任 MitM 证书；插件声明了解密域名。

## 说明

当前抓包没有记录开屏广告和首页购物信息流的实际投放接口，因此这两处还未覆盖。若仍看到广告，请从清空 Loon 请求记录后开始抓包，依次重启菜鸟（记录开屏）、停留并滚动首页购物信息流、打开包裹详情并滚动到广告区域，然后导出 HAR；这能帮助定位对应接口并补充精确规则。
