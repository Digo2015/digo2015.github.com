---
layout: page
title: one world express api 文档说明
tagline:  
description: test
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

1. [CreatePackage]({{ BASE_PATH }}2015/03/06/CreatePackage) ：上传一个包裹信息，同时申请一个包裹跟踪号。
2. [CancelPackage]({{ BASE_PATH }}#CancelPackage) ：取消并删除“交运”前的包裹信息。
3. [ConfirmPackage]({{ BASE_PATH }}#ConfirmPackage) ：对已上传包裹进行“交运”操作。
4. [GetShippingLabel]({{ BASE_PATH }}#GetShippingLabel) ：获取已上传包裹打印标签流。
5. [GetShippingPackage]({{ BASE_PATH }}#GetShippingPackage) ：获取已上传包裹详细信息。
7. [GetShippingRate]({{ BASE_PATH }}#GetShippingRate) ：根据包裹重量、保险、运输服务等获取运费信息。
8. [VerifyUser]({{ BASE_PATH }}#VerifyUser) ：验证API授权是否成功。
9. [GetTracking]({{ BASE_PATH }}#GetTracking)：根据ProcessCode获取包裹轨迹信息。


    
## 接入点

沙盒测试地址为：http://api.oneworldexpress.com/sandbox/v1/

正式运作地址为：http://api.oneworldexpress.com/product/v1/

### 创建包裹接口

功能：上传一个包裹信息，同时申请一个包裹跟踪号。
<div class="section" id="request">
<a name="CreatePackage"></a>
<h4>Request URL</h4>
<p>POST /api/parcels/create</P>
<h4>Request Headers</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
<colgroup>
<col width="20%">
<col width="40%">
<col width="40%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd">
<th class="head">名称</th>
<th class="head">值</th>
<th class="head">说明</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td>Token</td>
<td>HC-DX;A;C</td>
<td>开发者验证字符串</td>
</tr>
</tbody>
</table>
</div>
<h4>Request</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
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
<td>RefOrderNumber</td>
<td>String</td>
<td>必须</td>
<td>客户订单号</td>
<td>SO1503061000001</td>
</tr>
<tr class="row-odd">
<td>ShipToAddress</td>
<td><a class="reference internal" href="#Address"><em>Address</em></a></td>
<td>必须</td>
<td>收件人地址信息</td>
<td></td>
</tr>
<tr class="row-even">
<td>WeightInKG</td>
<td>decimal</td>
<td>必须</td>
<td>包裹重量(单位:KG)</td>
<td>1.580</td>
</tr>
<tr class="row-odd">
<td>DetailInfo</td>
<td><a class="reference internal" href="#ItemDetail"><em>ItemDetail</em></a>[]</td>
<td>必须</td>
<td>包裹内件明细</td>
<td></td>
</tr>
<tr class="row-even">
<td>TotalValue</td>
<td><a class="reference internal" href="#Amount"><em>Amount</em></a></td>
<td>必须</td>
<td>包裹总金额</td>
<td></td>
</tr>
<tr class="row-odd">
<td>WithBattery</td>
<td><a class="reference internal" href="#WithBatteryType"><em>WithBatteryType</em></a></td>
<td>必须</td>
<td>包裹是否含有带电产品</td>
<td></td>
</tr>
<tr class="row-even">
<td>TotalValue</td>
<td><a class="reference internal" href="#Amount"><em>Amount</em></a></td>
<td>必须</td>
<td>包裹总金额</td>
<td></td>
</tr>
<tr class="row-odd">
<td>CubeSize</td>
<td><a class="reference internal" href="#TotalVolume"><em>CubeSize</em></a></td>
<td>必须</td>
<td>包裹尺寸(长*宽*高)</td>
<td></td>
</tr>
<tr class="row-even">
<td>Notes</td>
<td>string</td>
<td></td>
<td>包裹备注</td>
<td></td>
</tr>
<tr class="row-odd">
<td>BatchNo</td>
<td>string</td>
<td></td>
<td>批次</td>
<td></td>
</tr>
<tr class="row-even">
<td>ShippingMethod</td>
<td>string</td>
<td></td>
<td>发货方式</td>
<td></td>
</tr>
<tr class="row-odd">
<td>ItemType</td>
<td><a class="reference internal" href="#ItemType"><em>ItemType</em></a></td>
<td>必须</td>
<td>包裹类型</td>
<td></td>
</tr>
<tr class="row-even">
<td>DutyPaymentMethod</td>
<td><a class="reference internal" href="#DutyPaymentMethod"><em>DutyPaymentMethod</em></a></td>
<td>必须</td>
<td>结算方式</td>
<td></td>
</tr>
<tr class="row-odd">
<td>TrackingNumber</td>
<td>string</td>
<td></td>
<td>预分配挂号</td>
<td></td>
</tr>
<tr class="row-even">
<td>MPS</td>
<td>bool</td>
<td></td>
<td>快递一票多件(multiple package shipment)</td>
<td></td>
</tr>
<tr class="row-odd">
<td>CheckRepeat</td>
<td>bool</td>
<td></td>
<td>检查包裹是否重复</td>
<td></td>
</tr>
<tr class="row-even">
<td>Cases</td>
<td><a class="reference internal" href="#CaseInfo"><em>CaseInfo</em></a>[]</td>
<td></td>
<td>快递一票多件,箱子列表</td>
<td></td>
</tr>

</tbody>
</table>
</div>
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
	<td>ProcessCode</td>
	<td>string</td>
	<td>One World包裹处理号</td>
	<td>OW1503061000001</td>
</tr>
<tr class="row-odd">
	<td>ReferenceId</td>
	<td>string</td>
	<td>客户订单号</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>TrackingNumber</td>
	<td>string</td>
	<td>挂号</td>
	<td></td>
</tr>
<tr class="row-odd">
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
<tr class="row-odd">
	<td>Message</td>
	<td>string</td>
	<td>返回操作结果消息</td>
	<td>失败返回错误消息</td>
</tr>
<tr class="row-even">
	<td>Timestamp</td>
	<td>datetime</td>
	<td>调用时间(UTC)</td>
	<td>2015-03-06T04:00:26.503+0000</td>
</tr>
</tbody>
</table>
</div>
</div>

## 获取已上传包裹详细信息。

功能：根据处理号,获取已上传包裹详细信息。
<div class="section" id="request">
<a name="GetShippingPackage"></a>
<h4>Request URL</h4>
<p>GET /api/parcels/{processcode}</P>
<h4>Request Headers</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
<colgroup>
<col width="20%">
<col width="40%">
<col width="40%">
</colgroup>
<thead valign="bottom">
<tr class="row-odd">
<th class="head">名称</th>
<th class="head">值</th>
<th class="head">说明</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even">
<td>Token</td>
<td>HC-DX;A;C</td>
<td>开发者验证字符串</td>
</tr>
</tbody>
</table>
</div>
<h4>Request</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
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
<td>processCode</td>
<td>String</td>
<td>必须</td>
<td>包裹处理号</td>
<td>OW1503061000001</td>
</tr>
</tbody>
</table>
</div>
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
	<td>CustomerId</td>
	<td>string</td>
	<td>客户代码</td>
	<td>OW0001</td>
</tr>
<tr class="row-odd">
	<td>RefOrderNumber</td>
	<td>string</td>
	<td>客户订单号</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>ProcessCode</td>
	<td>string</td>
	<td>包裹处理号</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>ShipToAddress</td>
	<td><a class="reference internal" href="#Address"><em>Address</em></a></td>
	<td>收件人地址信息</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>ProcessCode</td>
	<td>string</td>
	<td>包裹处理号</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>Status</td>
	<td><a class="reference internal" href="#ParcelStatus"><em>ParcelStatus</em></a></td>
	<td>收件人地址信息</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>RealWeightInKG</td>
	<td>decimal</td>
	<td>包裹预报重量(单位:KG)</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>CheckWeightInKG</td>
	<td>decimal</td>
	<td>包裹复核重量(单位:KG)</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>DeclareInfo</td>
	<td><a class="reference internal" href="#ItemDetail"><em>ItemDetail</em></a>[]</td>
	<td>包裹预报申报信息</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>Value</td>
	<td><a class="reference internal" href="#ItemDetail"><em>Amount</em></a></td>
	<td>包裹申报金额</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>WithBattery</td>
	<td><a class="reference internal" href="#WithBattery"><em>WithBattery</em></a></td>
	<td>是否带电</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>Volume</td>
	<td><a class="reference internal" href="#CubeSize"><em>CubeSize</em></a></td>
	<td>包裹预报尺寸</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>RealVolume</td>
	<td><a class="reference internal" href="#CubeSize"><em>CubeSize</em></a></td>
	<td>包裹复核尺寸</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>Notes</td>
	<td>string</td>
	<td>包裹备注</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>BatchNo</td>
	<td>string</td>
	<td>批次</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>ProcessLocation</td>
	<td>string</td>
	<td>操作中心</td>
	<td>SZ</td>
</tr>
<tr class="row-even">
	<td>ShippingMethod</td>
	<td><a class="reference internal" href="#ShippingMethod"><em>ShippingMethod</em></a></td>
	<td>发货方式</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>ItemType</td>
	<td><a class="reference internal" href="#ItemType"><em>ItemType</em></a></td>
	<td>包裹类型</td>
	<td>DOC,SPX</td>
</tr>
<tr class="row-even">
	<td>DutyPaymentMethod</td>
	<td><a class="reference internal" href="#DutyPaymentMethod"><em>DutyPaymentMethod</em></a></td>
	<td>结算方式</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>RealShippingMethod</td>
	<td><a class="reference internal" href="#ShippingMethod"><em>ShippingMethod</em></a></td>
	<td>发货方式</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>TrackingNumber</td>
	<td>string</td>
	<td>挂号</td>
	<td></td>
</tr>
<tr class="row-odd">
	<td>RealTrackingNumber</td>
	<td>string</td>
	<td>挂号</td>
	<td></td>
</tr>
<tr class="row-even">
	<td>IsMPS</td>
	<td>string</td>
	<td>快递一票多件(multiple package shipment)</td>
	<td></td>
</tr>

<tr class="row-odd">
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
<tr class="row-odd">
	<td>Message</td>
	<td>string</td>
	<td>返回操作结果消息</td>
	<td>失败返回错误消息</td>
</tr>
<tr class="row-even">
	<td>Timestamp</td>
	<td>datetime</td>
	<td>调用时间(UTC)</td>
	<td>2015-03-06T04:00:26.503+0000</td>
</tr>
</tbody>
</table>
</div>
</div>

## 用户验证接口
功能：验证用户是否授权成功。
<div class="section" id="request">
<a name="VerifyUser"></a>
<h4>Request URL</h4>
<p>GET /api/VerifyUser</P>
<h4>Request</h4>
<div class="wy-table-responsive">
<table border="1" class="docutils">
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
	<td>调用时间(UTC)</td>
	<td>2015-03-06T04:00:26.503+0000</td>
</tr>
</tbody>
</table>
</div>
</div>

<!--
<ul class="posts">
  {% for post in site.posts %}
    <li><span>{{ post.date | date_to_string }}</span> &raquo; <a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></li>
  {% endfor %}
</ul>
-->


