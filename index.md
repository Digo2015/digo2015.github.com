---
layout: page
title: one world express api 文档说明
tagline:  
description: 
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
<td>Authorization</td>
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

### sample
	{
    "RefOrderNumber": "REF0000000001",
    "ShipToAddress": {
        "Company": "Company",
        "Street1": "Street1",
        "Street2": "Street1",
        "Street3": null,
        "City": "Cite",
        "Province": "GD",
        "Country": "China",
        "CountryCode": "CN",
        "Postcode": "100001",
        "Contacter": "Contacter01",
        "Tel": "134567890",
        "Email": ""
    },
    "WeightInKG": 1.5,
    "DetailInfo": [
        {
            "GoodsID": "GoodsID",
            "GoodsTitle": "GoodsTitle",
            "NameEN": "Test",
            "NameCN": "品名测试",
            "DeclaredValue": {
                "Currency": "USD",
                "Value": 15
            },
            "WeightInKG": 1.5,
            "QTY": 1,
            "HSCode": "HSCode",
            "CaseCode": "Box001"
        }
    ],
    "TotalValue": {
        "Currency": "USD",
        "Value": 35
    },
    "WithBattery": 0,
    "TotalVolume": {
        "Length": 1,
        "Wdith": 1,
        "Height": 1,
        "Unit": "CM"
    },
    "Notes": "Test",
    "BatchNo": "",
    "ShippingMethod": "REGPOST",
    "ItemType": "SPX",
    "DutyPaymentMethod": "DDU",
    "TrackingNumber": "",
    "MPS": true,
    "CheckRepeat": false,
    "Cases": [
        {
            "Code": "Box001",
            "WeightInKG": 10,
            "Volume": {
                "Length": 8,
                "Wdith": 5,
                "Height": 4,
                "Unit": "CM"
            }
        }
    ]
	}
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
<td>Authorization</td>
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
<td><a class="reference internal" href="#Volume"><em>Amount</em></a></td>
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

###结果
	{
    "Data": {
        "ParcelInfo": {
            "CustomerId": "OW00004",
            "RefOrderNumber": "REF0000000001",
            "ProcessCode": "OW2015022600000",
            "ShipToAddress": {
                "Company": "Company",
                "Street1": "Street1",
                "Street2": "Street1",
                "Street3": "",
                "City": "Cite",
                "Province": "GD",
                "Country": "China",
                "CountryCode": "CN",
                "Postcode": "100001",
                "Contacter": "Contacter01",
                "Tel": "134567890",
                "Email": ""
            },
            "Status": "InSock",
            "RealWeightInKG": 1.5,
            "CheckWeightInKG": 0,
            "DeclareInfo": [
                {
                    "GoodsID": "GoodsID",
                    "GoodsTitle": "GoodsTitle",
                    "NameEN": "Test",
                    "NameCN": "品名测试",
                    "DeclaredValue": {
                        "Currency": "USD",
                        "Value": 15
                    },
                    "WeightInKG": 1.5,
                    "QTY": 1,
                    "HSCode": "HSCode",
                    "CaseCode": "Box001"
                }
            ],
            "Value": {
                "Currency": "USD",
                "Value": 35
            },
            "WithBattery": "NOBattery",
            "Volume": {
                "Length": 1,
                "Wdith": 1,
                "Height": 1,
                "Unit": "CM"
            },
            "RealVolume": {
                "Length": 1,
                "Wdith": 1,
                "Height": 1,
                "Unit": "CM"
            },
            "Notes": "TEst",
            "BatchNo": "",
            "ProcessLocation": "SZ",
            "ShippingMethod": {
                "Code": "REGPOST",
                "Name": "SW专线（欧洲）",
                "IsTracking": true,
                "ISVolumeWeight": true,
                "MaxVolumeWeightInCM": 0,
                "MaxWeightInKG": 0
            },
            "ItemType": "SPX",
            "DutyPaymentMethod": "DDU",
            "RealShippingMethod": {
                "Code": "REGPOST",
                "Name": "SW专线（欧洲）",
                "IsTracking": true,
                "ISVolumeWeight": true,
                "MaxVolumeWeightInCM": 0,
                "MaxWeightInKG": 0
            },
            "TrackingNumber": "",
            "RealTrackingNumber": "",
            "IsMPS": true
        }
    },
    "Succeeded": true,
    "Error": null
	}

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

## 数据类型

<div class="section" id="request">
<a name="Address"></a>
<h4>Address</h4>
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
<td>Company</td>
<td>String</td>
<td></td>
<td>联系人公司</td>
<td></td>
</tr>
<tr class="row-odd">
<td>Street1</td>
<td>String</td>
<td>必须</td>
<td>街道1</td>
<td></td>
</tr>
<tr class="row-even">
<td>Street2</td>
<td>String</td>
<td></td>
<td>街道2</td>
<td></td>
</tr>
<tr class="row-odd">
<td>Street3</td>
<td>String</td>
<td></td>
<td>街道3</td>
<td></td>
</tr>
<tr class="row-even">
<td>City</td>
<td>String</td>
<td>必须</td>
<td>城市</td>
<td></td>
</tr>
<tr class="row-odd">
<td>Province</td>
<td>String</td>
<td>必须</td>
<td>州/省</td>
<td></td>
</tr>
<tr class="row-even">
<td>Country</td>
<td>String</td>
<td>必须</td>
<td>国家英文名称</td>
<td></td>
</tr>
<tr class="row-odd">
<td>CountryCode</td>
<td>String</td>
<td>必须</td>
<td>国家代码</td>
<td>US</td>
</tr>
<tr class="row-even">
<td>Postcode</td>
<td>String</td>
<td>必须</td>
<td>邮编</td>
<td></td>
</tr>
<tr class="row-odd">
<td>Contacter</td>
<td>String</td>
<td>必须</td>
<td>收件人</td>
<td>zhangsan</td>
</tr>
<tr class="row-even">
<td>Tel</td>
<td>String</td>
<td>必须</td>
<td>收件联系电话</td>
<td></td>
</tr>
<tr class="row-odd">
<td>Email</td>
<td>String</td>
<td>必须</td>
<td>收件人邮箱</td>
<td>zhangsan@gmail.com</td>
</tr>
</tbody>
</table>
</div>
</div>


<div class="section" id="request">
    <a name="ItemDetail"></a>
<h4>ItemDetail</h4>
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
<td>GoodsID</td>
<td>String</td>
<td></td>
<td>货物编号</td>
<td>如SKU,库存编号</td>
</tr>
<tr class="row-odd">
<td>GoodsTitle</td>
<td>String</td>
<td>必须</td>
<td>货物描述</td>
<td></td>
</tr>
<tr class="row-even">
<td>NameEN</td>
<td>String</td>
<td>必须</td>
<td>英文申报名称</td>
<td></td>
</tr>
<tr class="row-odd">
<td>NameCN</td>
<td>String</td>
<td></td>
<td>中文申报名称</td>
<td></td>
</tr>
<tr class="row-even">
<td>DeclaredValue</td>
<td><a class="reference internal" href="#Amount"><em>Amount</em></a></td>
<td>必须</td>
<td>申报价值</td>
<td></td>
</tr>
<tr class="row-odd">
<td>WeightInKG</td>
<td>decimal</td>
<td>必须</td>
<td>申报重量(KG)</td>
<td>1.5</td>
</tr>
<tr class="row-even">
<td>QTY</td>
<td>int</td>
<td>必须</td>
<td>申报数量</td>
<td></td>
</tr>
<tr class="row-odd">
<td>HSCode</td>
<td>String</td>
<td></td>
<td>海关编码</td>
<td></td>
</tr>
<tr class="row-even">
<td>CaseCode</td>
<td>String</td>
<td></td>
<td>箱号(一票多件)</td>
<td>Box123</td>
</tr>
</tbody>
</table>
</div>
</div>


<div class="section" id="request">
<a name="Amount"></a>
<h4>Amount</h4>
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
<td>Currency</td>
<td>int</td>
<td>必须</td>
<td>货币类型</td>
<td>0=USD, 1=GBP, 2=CNY</td>
</tr>
<tr class="row-odd">
<td>Value</td>
<td>decimal</td>
<td>必须</td>
<td>金额</td>
<td></td>
</tr>
</tbody>
</table>
</div>
</div>

<div class="section" id="request">
<a name="CubeSize"></a>
<h4>CubeSize</h4>
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
<td>Height</td>
<td>decimal</td>
<td>必须</td>
<td>高</td>
<td>1</td>
</tr>
<tr class="row-odd">
<td>Length</td>
<td>decimal</td>
<td>必须</td>
<td>长</td>
<td>1</td>
</tr>
<tr class="row-even">
<td>Wdith</td>
<td>decimal</td>
<td>必须</td>
<td>宽</td>
<td>1</td>
</tr>
<tr class="row-odd">
<td>Unit</td>
<td>int</td>
<td>必须</td>
<td>计量单位</td>
<td>0=CM, 1=M</td>
</tr>

</tbody>
</table>
</div>
</div>

<div class="section" id="request">
<a name="CaseInfo"></a>
<h4>CaseInfo</h4>
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
<td>Code</td>
<td>decimal</td>
<td>必须</td>
<td>箱号</td>
<td>Box001</td>
</tr>
<tr class="row-odd">
<td>WeightInKG</td>
<td>decimal</td>
<td>必须</td>
<td>箱子重量</td>
<td>2.5</td>
</tr>
<tr class="row-even">
<td>Volume</td>
<td><a class="reference internal" href="#CubeSize"><em>CubeSize</em></a></td>
<td>必须</td>
<td>体积</td>
<td></td>
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


