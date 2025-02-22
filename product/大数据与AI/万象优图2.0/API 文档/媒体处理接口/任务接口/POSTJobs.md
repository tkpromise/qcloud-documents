## 功能描述
用于提交一个新任务。

## 请求
### 请求示例

```shell
POST /jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

> Authorization: Auth String （详情请查阅 [请求签名](https://cloud.tencent.com/document/product/436/7778) 文档）。


### 请求头

此接口仅使用公共请求头部，详情请参见 [公共请求头部](https://cloud.tencent.com/document/product/436/7728) 文档。

### 请求体
该请求操作的实现需要有如下请求体。

```shell
<Request>
  <Tag></Tag>
  <Input>
    <Object></Object>
  </Input>
  <Operation>
    <TemplateId></TemplateId>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
  </Operation>
  <QueueId></QueueId>
</Request>
```

具体的数据描述如下：

<table>
   <tr>
      <th nowrap="nowrap">节点名称（关键字）</th>
      <th>父节点</th>
      <th>描述</th>
      <th>类型</th>
      <th>是否必选</th>
   </tr>
   <tr>
      <td>Request</td>
      <td>无</td>
      <td>保存请求的容器</td>
      <td>Container</td>
      <td>是</td>
   </tr>
</table>

Container 类型 Request 的具体数据描述如下：

<table>
   <tr>
      <th nowrap="nowrap">节点名称（关键字）</th>
      <th>父节点</th>
      <th>描述</th>
      <th>类型</th>
      <th>是否必选</th>
   </tr>
   <tr>
      <td>Tag</td>
      <td>Request</td>
      <td>创建任务的 Tag：Animation 或者 Snapshot。</td>
      <td>String</td>
      <td>是</td>
   </tr>
   <tr>
      <td>Input</td>
      <td>Request</td>
      <td>待操作的媒体信息</td>
      <td>Container</td>
      <td>是</td>
   </tr>
   <tr>
      <td>Operation</td>
      <td>Request</td>
      <td>操作规则</td>
      <td>Container</td>
      <td>是</td>
   </tr>
   <tr>
      <td>QueueId</td>
      <td>Request</td>
      <td>任务所在的队列 ID</td>
      <td>String</td>
      <td>是</td>
   </tr>
</table>

Container 类型 Input 的具体数据描述如下：
<table>
   <tr>
      <th nowrap="nowrap">节点名称（关键字）</th>
      <th>父节点</th>
      <th>描述</th>
      <th>类型</th>
      <th>是否必选</th>
   </tr>
   <tr>
      <td>Object</td>
      <td>Request.Input</td>
      <td>媒体文件的名称</td>
      <td>String</td>
      <td>是</td>
   </tr>
</table>

Container 类型 Operation 的具体数据描述如下：
<table>
   <tr>
      <th nowrap="nowrap">节点名称（关键字）</th>
      <th>父节点</th>
      <th>描述</th>
      <th>类型</th>
      <th>是否必选</th>
   </tr>
   <tr>
      <td>TemplateId</td>
      <td>Request.Operation</td>
      <td>指定的模版 ID</td>
      <td>String</td>
      <td>是</td>
   </tr>
   <tr>
      <td>Output</td>
      <td>Request.Operation</td>
      <td>结果输出地址</td>
      <td>Container</td>
      <td>是</td>
   </tr>
</table>


## 响应
### 响应头

此接口仅返回公共响应头部，详情请参见 [公共响应头部](https://cloud.tencent.com/document/product/436/7729) 文档。

### 响应体
该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

```
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <QueueId></QueueId>
    <Tag><Tag>
    <Input>
      <Object></Object>
    </Input>
    <Operation>
      <TemplateId></TemplateId>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
      <MediaInfo>
      </MeidaInfo>
    </Operation>
  </JobsDetail>
</Response>
```

具体的数据内容如下：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| Response |无| 保存结果的容器 | Container |

Container 节点 Response 的内容：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| JobsDetail | Response | 任务的详细信息 |  Container |


Container 节点 JobsDetail 的内容：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| Code | Response.JobsDetail | 错误码，只有 State 为 Failed 时有意义 |  String |
| Message | Response.JobsDetail | 错误描述，只有 State 为 Failed 时有意义 |  String |
| JobId | Response.JobsDetail | 新创建任务的 ID |  String |
| Tag | Response.JobsDetail | 新创建任务的Tag：Animation 或者 Snapshot。 | String |
| State | Response.JobsDetail | 任务的状态，为 Submitted、Running、Success、Failed、Pause、Cancel 其中一个 |  String |
| CreationTime | Response.JobsDetail | 任务的创建时间 |  String |
| QueueId | Response.JobsDetail | 任务所属的队列 ID |  String |
| Input | Response.JobsDetail | 该任务的输入资源地址 |  Container |
| Operation | Response.JobsDetail | 该任务的规则 |  Container |

Container 节点 Input 的内容：
同上面请求中的 Request.Input 节点。

Container 节点 Operation 的内容：

|节点名称（关键字）|父节点|描述|类型|
|:---|:-- |:--|:--|
| TemplateId | Response.JobsDetail.Operation | 任务的模版 ID |  String |
| Output | Response.JobsDetail.Operation | 文件的输出地址 |  Container |
| MediaInfo | Response.JobsDetail.Operation | 转码输出视频的信息，没有时不返回 |  Container |

Container 节点 Output 的内容：
同上面请求中的 Request.Operation.Output 节点。

Container 节点 MediaInfo 的内容：
同 [GenerateMediaInfo](#插入GenerateMediaInfo文档链接) 接口中的 Response.MediaInfo 节点。

### 错误码
常见的错误信息请参见 [错误码](https://cloud.tencent.com/document/product/436/7730) 文档。


## 实际案例

### 请求

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>Snapshot<Tag>
  <Input>
    <Object>test.mp4</Object>
  </Input>
  <Operation>
    <TemplateId>taaaabkkenskdixxkskdf</TemplateId>
    <Output>
      <Region>ap-guangzhou</Region>
      <Bucket>abc-1250000001</Bucket>
      <Object>test-trans.mkv</Object>
    </Output>
  </Operation>
  <QueueId>pssefffensldddsfessgg</QueueId>
</Request>
```

### 响应

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=

<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>jabcsdssfeipplsdfwe</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <QueueId>pssefffensldddsfessgg</QueueId>
    <Tag>Snapshot<Tag>
    <Input>
      <Object>test.mp4</Object>
    </Input>
    <Operation>
      <TemplateId>taaaabkkenskdixxkskdf</TemplateId>
      <Output>
        <Region>ap-guangzhou</Region>
        <Bucket>abc-1250000001</Bucket>
        <Object>test-trans.mkv</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```


