---
layout: page
title: one world express api 文档说明
tagline:  
---
{% include JB/setup %}


[使用教程](http://api.oneworldexpress.com/usages)

## API 对接指南

### 简要概述 ###
通过one world express API，您可以方便的将您自己的应用连结到one world express的服务上，使得操作更便捷、更符合您自己的需要。

### 特征

格式：WEB API<br/>
协议：HTTP GET 及 POST<br/>
版本：V1<br/>

### API列表

1. [CreatePackage]({{ BASE_PATH }}#CreatePackage) ：上传一个包裹信息，同时申请一个包裹跟踪号。
2. [CancelPackage]({{ BASE_PATH }}#CancelPackage) ：取消并删除“交运”前的包裹信息。
3. [ConfirmPackage]({{ BASE_PATH }}#ConfirmPackage) ：对已上传包裹进行“交运”操作。
4. [GetShippingLabel]({{ BASE_PATH }}#GetShippingLabel) ：获取已上传包裹打印标签流。
5. [GetShippingPackage]({{ BASE_PATH }}#GetShippingPackage) ：获取已上传包裹详细信息。
7. [GetShippingRate]({{ BASE_PATH }}#GetShippingRate) ：根据包裹重量、保险、运输服务等获取运费信息。
8. [VerifyUser]({{ BASE_PATH }}#VerifyUser) ：验证API授权是否成功。
9. [GetTrackingNumber]({{ BASE_PATH }}#GetTrackingNumber)：根据ProcessCode取回一个包裹的跟踪号。


    
## 接入点

沙盒测试地址为：http://api.oneworldexpress.com/sandbox/v1/

正式运作地址为：http://api.oneworldexpress.com/product/v1/


## 用户验证接口
<div class="section" id="request">
<h4>Request</h4><a name="CreatePackage"></a>
<div class="wy-table-responsive"><table border="1" class="docutils">
<colgroup>
	<col width="11%">
	<col width="10%">
	<col width="13%">
	<col width="23%">
	<col width="43%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd">
	<th class="head">名称</th>
	<th class="head">类型</th>
	<th class="head">是否必须</th>
	<th class="head">描述</th>
	<th class="head">示例值</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td>Token</td>
<td>String</td>
<td>必须</td>
<td>开发者验证字符串</td>
<td>887E99B5F89BB18BEA12B204B620D236</td>
</tr>
<tr class="row-odd">
<td>UserKey</td>
<td>String</td>
<td>必须</td>
<td>用户验证字符串</td>
<td>wr5qjqh4gj</td>
</tr>
<tr class="row-even">
<td>UserID</td>
<td>String</td>
<td>必须</td>
<td>用户登陆名</td>
<td>guest</td>
</tr>
</tbody>
</table></div>
</div>

<div class="section" id="response">
<h4>Response</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
<colgroup>
	<col width="12%">
	<col width="33%">
	<col width="37%">
	<col width="18%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd">
	<th class="head">名称</th>
	<th class="head">类型</th>
	<th class="head">描述</th>
	<th class="head">示例值</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even">
	<td>Version</td>
	<td>string</td>
	<td>API调用版本</td>
	<td>V1</td>
</tr>
<tr class="row-even">
	<td>Ack</td>
	<td><a class="reference internal" href="#enumack"><em>EnumAck</em></a></td>
	<td>返回操作是否成功</td>
	<td>Success</td>
</tr>
<tr class="row-even">
	<td>Message</td>
	<td>string</td>
	<td>返回操作结果消息</td>
	<td>失败返回错误消息</td>
</tr>
<tr class="row-even">
	<td>Timestamp</td>
	<td>datetime</td>
	<td>调用时间</td>
	<td>2015-03-10T12:00:00.100</td>
</tr>
</tbody>
</table>
</div>
</div>

<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>


