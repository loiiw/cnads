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
| `api-access.pangolin-sdk-toutiao.com` | 穿山甲开屏广告请求（`/api/ad/union/sdk/get_ads/`） |
| `sdk.1rtb.net` | 广告请求（`/sdk/req_ad`） |
| `entry-su1.ubixioe.com` | 广告 SDK 请求（`/mob/sdk/v2/endpoint`） |
| `adx-cfg-u1.ubixioe.com` | Ubixioe 广告 SDK 初始化配置 |
| `win.gdt.qq.com` | 腾讯广告 SDK 请求（`/win_notice.fcg`） |
| `*.pglstatp-toutiao.com/obj/ad-pattern/`、`lf-cdn-tos.bytescm.com/obj/static/ad/` | 穿山甲广告素材和交互资源 |
| `cn-lde-mtop.cainiao.com` | 物流详情响应中移除 `data.globalData.formerModel.extPackageAttr.ADS_QUERY_PARAM` |
| `e2e-mtop.cainiao.com` | 先删除含广告列表的整个开屏弹层项，再移除其他带 `materialId` 的素材项 |
| `netflow-mtop.cainiao.com`、`nbcps-mtop.cainiao.com` | 菜鸟广告展现与展示接口 |

广告服务域名使用 Loon 的域名拒绝规则。物流详情和开屏响应改写需要在 Loon 中启用 HTTPS 解密并信任 MitM 证书；插件声明了解密域名。

## 说明

规则基于抓包中确认的开屏广告对象、物流详情广告参数和专用广告服务接口。若仍有广告，请从清空 Loon 请求记录后开始抓包，依次重启菜鸟、停留并滚动首页购物信息流、打开包裹详情并滚动到广告区域，然后导出 HAR，以便继续定位未覆盖的广告来源。
