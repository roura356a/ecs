# AddTags {#AddTags .reference}

添加或者覆盖一个或者多个标签到云服务器 ECS 的各项资源上。您可以添加标签到实例、磁盘、快照、镜像、安全组等，便于管理资源。

## 描述 {#section_av1_byg_ydb .section}

调用该接口时，您需要注意：

-   单项云服务器 ECS 资源最多可以添加 10 个标签。
-   标签键（`Tag.n.Key`）与标签值（`Tag.n.Value`） 必须键值匹配。

-   如果标签键（`Tag.n.Key`）在指定的资源上已经存在，则使用新的标签值（`Tag.n.Value`）自动覆盖原标签值。


## 请求参数 {#section_mzx_3yg_ydb .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|Action|String|是|系统规定参数。取值：AddTags|
|RegionId|String|是|资源所在的地域。您可以调用 [DescribeRegions](intl.zh-CN/API参考/地域/DescribeRegions.md#) 查看最新的阿里云地域列表。|
|ResourceType|String|是|资源类型。取值范围：-   disk
-   instance
-   image
-   securitygroup
-   snapshot

以上取值均为小写。|
|ResourceId|String|是|要绑定标签的资源 ID。例如，当资源类型（`ResourceType`）为实例（`instance`）时，资源 ID 可以理解为实例 ID。|
|Tag.n.Key|String|是|标签键，`n` 的取值范围为 \[1, 5\]。最多支持 64 个字符。不支持 aliyun、acs、http:// 和 https:// 开头。不允许为空字符串。|
|Tag.n.Value|String|是|标签值，`n` 的取值范围为 \[1, 5\]。最多支持 128 个字符。不支持 aliyun、acs、http:// 和 https:// 开头。允许为空字符串。|

## 返回参数 {#section_f54_lk5_xdb .section}

全是公共返回参数。参阅 [公共参数](intl.zh-CN/API参考/调用方式/公共参数.md#commonResponseParameters)。

## 示例 { .section}

**请求示例** 

```
https://ecs.aliyuncs.com/?Action=AddTags
&ResourceId=s-946ntx4wr
&ResourceType=snapshot
&RegionId=cn-shenzhen
&Tag.1.Key=test
&Tag.1.Value=api
&<公共请求参数>
```

**返回示例** 

**XML 格式**

```
<AddTagsResponse>
    <RequestId>C46FF5A8-C5F0-4024-8262-B16B639225A0</RequestId>
</AddTagsResponse>
```

 **JSON 格式** 

```
{
  "RequestId": "C46FF5A8-C5F0-4024-8262-B16B639225A0"
}
```

## 错误码 {#ErrorCode .section}

以下为本接口特有的错误码。更多错误码，请访问 [API 错误中心](https://error-center.alibabacloud.com/status/product/Ecs)。

|错误代码|错误信息|HTTP 状态码|说明|
|:---|:---|:-------|:-|
|InvalidTag.Mismatch|The specified Tag.n.Key and Tag.n.Value are not match.|400|标签键（`Tag.n.Key`）与标签值（`Tag.n.Value`） 必须键值匹配。|
|InvalidTagCount|The specified tags are beyond the permitted range.|400|指定的标签数不能超过五个。|
|InvalidTagKey.Malformed|The specified Tag.n.Key is not valid.|400|指定的 `Tag.n.Key` 不合法。|
|InvalidTagValue.Malformed|The specified Tag.n.Value is not valid.|400|指定的 `Tag.n.Value`不合法。|
|OperationDenied.QuotaExceed|The quota of tags on resource is beyond permitted range.|400|单项云服务器 ECS 资源最多可以绑定 10 个标签。|
|InvalidResourceId.NotSupported|The specified ResourceId does not support tagging.|403|指定的资源不支持标签功能。|
|InvalidRegionId.NotFound|The RegionId provided does not exist in our records.|404|指定的 `RegionId` 不存在。|
|InvalidResourceId.NotFound|The specified ResourceId is not found in our records.|404|指定的 `ResourceId` 不存在。|
|InvalidResourceType.NotFound|The ResourceType provided does not exist in our records.|404|指定的 `ResourceType`不存在。|

