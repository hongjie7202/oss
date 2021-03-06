# PutBucketReferer {#reference_prc_ys5_tdb .reference}

PutBucketReferer接口用于设置存储空间（Bucket）的防盗链（Referer）。您可以使用此接口设置Referer的访问白名单以及是否允许Referer字段为空。

## 请求语法 {#section_yfn_hcw_bz .section}

```
PUT /?referer HTTP/1.1
Date: GMT Date
Content-Length：ContentLength
Content-Type: application/xml
Host: BucketName.oss.aliyuncs.com
Authorization: SignatureValue

<?xml version="1.0" encoding="UTF-8"?>
<RefererConfiguration>
<AllowEmptyReferer>true</AllowEmptyReferer >
    <RefererList>
        <Referer> http://www.aliyun.com</Referer>
        <Referer> https://www.aliyun.com</Referer>
        <Referer> http://www.*.com</Referer>
        <Referer> https://www.?.aliyuncs.com</Referer>
    </RefererList>
</RefererConfiguration>
```

## 请求元素 {#section_ujq_jcw_bz .section}

|名称|类型|是否必需|描述|
|:-|:-|:---|:-|
|RefererConfiguration|容器|是| 保存Referer配置内容的容器。

 子节点：AllowEmptyReferer，RefererList

 父节点：无

 |
|AllowEmptyReferer|枚举字符串|是| 指定是否允许Referer字段为空的请求访问。指定的配置将替换原配置。

 取值：true \(默认值），false

 父节点：RefererConfiguration

 |
|RefererList|容器|是| 保存Referer访问白名单的容器。

 **说明：** PutBucketReferer操作将用RefererList中的白名单列表覆盖之前配置的白名单列表。当您上传的RefererList为空时（不包含Referer请求元素），此操作会覆盖已配置的白名单列表，即删除之前配置的RefererList。

 父节点：RefererConfiguration

 子节点：Referer

 |
|Referer|字符串|否| 指定一条Referer访问白名单。

 父节点：RefererList

 |

## 示例 {#section_ovw_mcw_bz .section}

**请求示例（不包含Referer）**

```
PUT /?referer HTTP/1.1
Host: BucketName.oss.example.com
Content-Length: 247
Date: Fri, 04 May 2012 03:21:12 GMT
Authorization: OSS qn6qrrqxo2oawuk53otfjbyc:KU5h8YMUC78M30dXqf3JxrTZHiA=

<?xml version="1.0" encoding="UTF-8"?>
<RefererConfiguration>
<AllowEmptyReferer>true</AllowEmptyReferer >
< RefererList />
</RefererConfiguration>

```

**请求示例（包含Referer）**

```
PUT /?referer HTTP/1.1
Host: BucketName.oss.example.com
Content-Length: 247
Date: Fri, 04 May 2012 03:21:12 GMT
Authorization: OSS qn6qrrqxo2oawuk53otfjbyc:KU5h8YMUC78M30dXqf3JxrTZHiA=

<?xml version="1.0" encoding="UTF-8"?>
<RefererConfiguration>
<AllowEmptyReferer>true</AllowEmptyReferer >
< RefererList>
<Referer> http://www.aliyun.com</Referer>
<Referer> https://www.aliyun.com</Referer>
<Referer> http://www.*.com</Referer>
<Referer> https://www.?.aliyuncs.com</Referer>
</ RefererList>
</RefererConfiguration>

```

**返回示例**

```
HTTP/1.1 200 OK
x-oss-request-id: 534B371674E88A4D8906008B
Date: Fri, 04 May 2012 03:21:12 GMT
Content-Length: 0
Connection: keep-alive
Server: AliyunOSS
```

## SDK {#section_egl_m2c_5gb .section}

此接口所对应的各语言SDK如下：

-   [Java](../../../../../intl.zh-CN/SDK 参考/Java/防盗链.md)
-   [Python](../../../../../intl.zh-CN/SDK 参考/PHP/防盗链.md)
-   [PHP](../../../../../intl.zh-CN/SDK 参考/PHP/防盗链.md)
-   [Go](../../../../../intl.zh-CN/SDK 参考/Go/防盗链.md)
-   [C](../../../../../intl.zh-CN/SDK 参考/C/防盗链.md)
-   [.NET](../../../../../intl.zh-CN/SDK 参考/.NET/防盗链.md)
-   [Node.js](../../../../../intl.zh-CN/SDK 参考/Node.js/防盗链.md)
-   [Ruby](../../../../../intl.zh-CN/SDK 参考/Ruby/防盗链.md)

## 错误码 {#section_dsv_grs_qgb .section}

|错误码|HTTP 状态码|描述|
|:--|:-------|:-|
|AccessDenied|403|没有操作权限。只有Bucket的拥有者才能发起PutBucketReferer请求。|
|InvalidDigest|400|上传了Content-MD5请求头后，OSS会计算消息体的Content-MD5并检查一致性，如果不一致会返回此错误码。|

