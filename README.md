# API 文档

说明：

1. 如果需要传参，一律使用`POST`方法
2. 如果不需要传参，使用`GET`方法
3. Response的Content-Type：`application/json;charset=UTF-8`
4. `Post`时Request的Content-Type：`application/json;charset=UTF-8`
5. 返回的JSON格式如下：

+ 正确时，`code = 0`，`msg = 返回的数据结构` 例如：

```json
{
  "code": 0,
  "msg": {
    "orgName": "工商银行",
    "orgId": 1
  }
}
```

或

```json
{
  "code": 0,
  "msg": [
    {
      "orgName": "工商银行"
    },
    {
      "orgName": "建设银行"
    }
  ]
}
```

+ 错误时，`code > 0`，`msg = 错误的解释` 例如：

```json
{
  "code": 100,
  "msg": "缺少参数"
}
```

## 1. 用户相关

### 1.1 登录

+ URL:
    + `/public/login`
+ 参数：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | phone | string | 用户的手机号码 | 13812345678 |
  | verificationCode | string | 短信验证码  | 123456 |

+ 返回样例：

```json
{
  "msg": "登录成功",
  "code": 0
}
```

### 1.2 查看当前登录用户的信息

+ URL:
    + `/public/current-user`
+ 参数：无
+ 返回字段：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | phone | string | 用户的手机号码 | 13812345678 |
  | userName | string | 短信验证码  | 123456 |
  | orgId | long | 用户当前操作的企业ID  | 21438893910917166 |
  | orgName | string | 用户当前操作的企业名称  | 深圳钝点科技有限公司 |

+ 返回样例：

```json
{
  "msg": {
    "orgName": "深圳XX科技有限公司",
    "phone": "13800020303",
    "userName": "李四",
    "orgId": 21438893910917166
  },
  "code": 0
}
```

### 1.3 登出

+ URL:
    + `/public/logout`
+ 参数：无
+ 返回样例：

```json
{
  "msg": "登出成功",
  "code": 0
}
```

### 1.4 查看当前用户拥有哪些企业的权限

+ URL:
    + `/public/current-user-org-list`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "orgId": 21438893910917166,
      "orgName": "深圳XX科技有限公司",
      "role": "ADMIN"
    }
  ],
  "code": 0
}
```

## 2. 企业相关

### 2.1 添加企业信息

+ URL:
    + `/api/add-org`

+ 参数：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | orgName | string | 企业名称 | 某某有限公司 |
  | legalPersonName | string | 法定代表人姓名  | 张三 |
  | legalPersonIdType | string | 法定代表人证件类型 | ID_CARD |
  | legalPersonIdNumber | string | 法定代表人证件号 | 110100195501010255 |
  | uniformSocialCreditCode | string | 机构统一社会信用代码 | E015691256491EAS |
  | orgAddress | string | 机构地址 | 北京市朝阳区1号 |
  | startDate | string | 机构创立日期 | 2020-01-02 |
  | endDate | string | 企业经营到期时间（非必填） | 2020-01-02 |
  | bankAccount | string | 企业银行账号 | 6225558251498291981 |
  | bankName | string | 开户行 | 工商银行 |
  | businessScope | string | 经营范围 | 制药 |

+ 返回样例：

```json
{
  "msg": "企业保存成功",
  "code": 0
}
```

## 3. 枚举类型数据

### 3.1 货币ISO列表

+ URL:
    + `/public/currency-code`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "人民币",
      "name": "CNY"
    },
    {
      "displayName": "美元",
      "name": "USD"
    }
  ],
  "code": 0
}
```

### 3.2 支付方式

+ URL:
    + `/public/payment-type`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "现金银行转账",
      "name": "CASH_BANK_TRANSFER"
    },
    {
      "displayName": "现金支票",
      "name": "CASH_CHECK"
    },
    {
      "displayName": "现金第三方电子支付",
      "name": "CASH_TP_EPAY"
    },
    {
      "displayName": "商业承兑汇票",
      "name": "COMMERCIAL_DRAFT"
    }
  ],
  "code": 0
}
```

### 3.3 订单状态

+ URL:
    + `/public/order-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "未出货",
      "name": "NOT_SHIPPED"
    },
    {
      "displayName": "已出货",
      "name": "SHIPPED"
    },
    {
      "displayName": "已签收",
      "name": "RECEIVED"
    },
    {
      "displayName": "已支付",
      "name": "PAID"
    }
  ],
  "code": 0
}
```

### 3.4 个人证件类型

+ URL:
    + `/public/person-id-type`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "身份证",
      "name": "ID_CARD"
    },
    {
      "displayName": "护照",
      "name": "PASSPORT"
    },
    {
      "displayName": "台胞证",
      "name": "TAIWAN_RESIDENT"
    },
    {
      "displayName": "回乡证",
      "name": "HOME_RETURN"
    }
  ],
  "code": 0
}
```

### 3.5 资产类型

+ URL:
    + `/public/asset-type`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "商票质押",
      "name": "COM_DRAFT_PLEDGE"
    },
    {
      "displayName": "商票保理",
      "name": "COM_DRAFT_FACTORING"
    },
    {
      "displayName": "应收账款质押",
      "name": "RECEIVABLE_PLEDGE"
    },
    {
      "displayName": "应收账款保理",
      "name": "RECEIVABLE_FACTORING"
    }
  ],
  "code": 0
}
```

### 3.6 资产状态

+ URL:
    + `/public/asset-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "新提交",
      "name": "0"
    },
    {
      "displayName": "已发起融资",
      "name": "1"
    },
    {
      "displayName": "已匹配",
      "name": "2"
    },
    {
      "displayName": "已取消",
      "name": "-1"
    }
  ],
  "code": 0
}
```

### 3.7 确权状态

+ URL:
    + `/public/confirm-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "未确权",
      "name": "NOT_CONFIRMED"
    },
    {
      "displayName": "已确权",
      "name": "CONFIRMED"
    },
    {
      "displayName": "确权失败",
      "name": "FAILED"
    },
    {
      "displayName": "自动产生物权凭证",
      "name": "AUTO_CONFIRMED"
    }
  ],
  "code": 0
}
```

### 3.8 应收账款状态

+ URL:
    + `/public/receivable-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "已产生",
      "name": "CREATED"
    },
    {
      "displayName": "已登记",
      "name": "REGISTERED"
    },
    {
      "displayName": "已验证",
      "name": "VERIFIED"
    },
    {
      "displayName": "已确权",
      "name": "CONFIRMED"
    },
    {
      "displayName": "待审核",
      "name": "PENDING"
    },
    {
      "displayName": "已抵押",
      "name": "PLEDGED"
    },
    {
      "displayName": "已回款",
      "name": "COLLECTED"
    },
    {
      "displayName": "部分回款",
      "name": "PARTIAL_COLLECTED"
    },
    {
      "displayName": "已到期",
      "name": "EXPIRED"
    },
    {
      "displayName": "未知",
      "name": "UNKNOWN"
    }
  ],
  "code": 0
}
```

### 3.9 用户角色

+ URL:
    + `/public/role`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "法定代表人",
      "name": "LEGAL_PERSON"
    },
    {
      "displayName": "管理员",
      "name": "ADMIN"
    }
  ],
  "code": 0
}
```

### 3.10 商票状态

+ URL:
    + `/public/com-draft-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName": "出票已登记",
      "name": "SH_010004"
    },
    {
      "displayName": "提示承兑待签收",
      "name": "SH_020001"
    },
    {
      "displayName": "提示承兑已签收",
      "name": "SH_020006"
    }
  ],
  "code": 0
}
```

### 3.11 发票类型

+ URL:
    + `/public/invoice-type`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {
      "displayName":"增值税普通发票","name":"GENERAL_VAT_INVOICE"
    },
    {
      "displayName":"增值税专用发票","name":"SPECIAL_VAT_INVOICE"
    }
  ],"code":0}
```

### 3.12 合同状态

+ URL:
    + `/public/contract-status`
+ 参数：无
+ 返回样例：

```json
{
  "msg": [
    {"displayName":"新提交","name":"CREATED"},
    {"displayName":"完成初审","name":"PRELIMINARY_AUDITED"},
    {"displayName":"完成审核","name":"AUDITED"},
    {"displayName":"审核不通过","name":"AUDIT_FAILED"}
  ],
  "code":0
}
```

## 4. 资产

### 4.1 新建应收账款

+ URL:
    + `/api/add-receivable`
+ 参数： 
 
 | 参数名 | 类型 | 解释 | 例 | 
 | --- | --- | --- | --- | 
 | assetType | string | 资产类型 | RECEIVABLE_PLEDGE | 
 | assetAmount | decimal | 资产总额 | 1000000 | 
 | currencyCode | string | 货币ISO编号 | CNY | 
 | expireDate | string | 资产到期日期 | 2022-04-01 | 
 | issuerId | long | 债务人ID(非必填) | 123456 | 
 | issuerName | String | 债务人名称 | 某某有限公司 | 
 | assetSellerName | string | 债权人名称 | 某某有限公司 | 
 | receivableAmount | decimal | 应收账款总额 | 1000000 | 
 | paymentDate | string | 支付日期 | 2021-05-01 | 
 | paymentType | string | 付款方式 | CASH_CHECK | 
 | receivableStatus | string | 应收账款状态 | CREATED | 
 | comments | string | 备注 | |

+ 返回样例：

```json
{
  "msg": "应收账款保存成功",
  "code": 0
}
```

### 4.2 新建商票

+ URL:
  + `/api/add-com-draft`
+ 参数：

| 参数名 | 类型 | 解释 | 例 | 
| --- | --- | --- | --- | 
| assetType | string | 资产类型 | RECEIVABLE_PLEDGE | 
| assetAmount | decimal | 资产总额 | 1000000 | 
| currencyCode | string | 货币ISO编号 | CNY | 
| expireDate | string | 资产到期日期 | 2022-04-01 | 
| issuerId | long | 债务人ID(非必填) | 123456 | 
| issuerName | String | 债务人名称 | 某某有限公司 | 
| assetSellerName | string | 债权人名称 | 某某有限公司 | 
| cdAmount | decimal | 应收账款总额 | 1000000 | 
| issueDate | string | 出票日期 | 2021-05-01 | 
| maturityDate | string | 到期时间 | 2021-05-01 | 
| issuerBankName | string | 债务人开户行 | 工商银行 | 
| issuerAccountNumber | string | 债务人银行账号 | 62206155821586520552 | 
| assetSellerBankName | string | 债权人开户行 | 工商银行 | 
| assetSellerAccountNumber | string | 债权人银行账号 | 62206155821586520552 |
| cdCode | string | 商票编号 | 12319649106589196106056159 | 
| cdStatus | string | 商票状态 | SH_010004 | 
| acceptorName | string | 承兑人全称 | 某某有限公司 | 
| acceptorBankName | string | 承兑人开户行 | 工商银行 | 
| acceptorAccountNumber | string | 承兑人银行账号 | CASH_CHECK | 
| isTransferable | bool | 是否可转让 | true | 
| issuerCommit | string | 出票人承诺 | 到期承诺支付 | 
| acceptorCommit | string | 承兑人承诺 | 到期承诺支付 | 
| guarantorName | string | 保证人名称 | 某某公司 | 
| guarantorAddress | string | 保证人地址 | 北京市东城区1号 | 
| guaranteeDate | Date | 保证日期 | 2021-05-01 | 
| comments | string | 备注 | |

+ 返回样例：

```json
{
  "msg": "商票保存成功",
  "code": 0
}
```

### 4.3 资产方发布自己的资产

+ URL:
    + `/api/publish-my-asset`
+ 参数：

| 参数名 | 类型 | 解释 | 例 | 
| --- | --- | --- | --- | 
| assetId | long | 资产编号 | 21538211204431918 | 
| assetGroupName | string | 发布资产的名称 | 格力集团商票资产1000万 |
| offerInterestRate | decimal | 期望的利率 | 0.05 |
| offerAmount | decimal | 期望的融资总额 | 10000.00 |
| listingEndTime | datetime | 报价失效时间 | 2022-09-01 15:00:00 |
| comments | string | 备注 | |

+ 返回样例：

```json
{
  "msg": "资产发布成功",
  "code": 0
}
```

## 5. 单据相关

### 5.1 添加订单

+ URL:
    + `/api/add-order`

+ 参数：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | orderCode | string | 用户自定的订单编号 | 13812345678 |
  | orderDate | string | 订单签订日期  | 2021-05-03 |
  | buyerId | long | 订单买方的ID(非必填) | 1234567890 |
  | sellerId | long | 订单卖方的ID(非必填) | 1234567890 |
  | buyerName | String | 订单买方的名称 | 某某有限公司 |
  | sellerName | String | 订单卖方的名称 | 某某有限公司 |
  | itemList | list | 订单的内容 必须包含(itemCode, itemName, itemQuantity, unit, unitPrice, itemAmount) | [{"itemCode": "A01", "itemName": "PC", "itemQuantity": "10", "unit": "台", "unitPrice": "10000.00", "itemAmount": "100000"}] |
  | currencyCode | String | 货币ISO代码 | CNY |
  | shipping_date | String | 预计交货日期 | 2021-05-03 |
  | payment_date | String | 预计付款日期 | 2021-06-03 |
  | payment_type | String | 支付方式 | COMMERCIAL_DRAFT |
  | shipping_method | String | 送货方式 | 物流 |
  | shipping_company | String | 送货公司 | 顺丰 |
  | order_status | String | 订单状态 | SHIPPED |
  | comments | String | 备注(非必填) |  |

+ 返回样例：

```json
{
  "msg": "订单保存成功",
  "code": 0
}
```

### 5.2 添加发票

+ URL:
    + `/api/add-invoice`

+ 参数：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | invoiceType | string | 发票类型 | SPECIAL_VAT_INVOICE |
  | invoiceCode | string | 发票代码  | 1101254788925125 |
  | invoiceNumber | string | 发票号码 | 0000001 |
  | invoiceNetAmount | decimal | 发票除税外的金额 | 1234567890.00 |
  | invoiceTaxAmount | String | 发票除税款的金额 | 某某有限公司 |
  | invoiceDate | string | 开票日期 | 2021-05-03 |
  | buyerId | string | 买方ID(非必填) | 某某公司 |
  | sellerId | string | 卖方ID(非必填) | 某某公司 |
  | buyerName | string | 买方名称 | 某某公司 |
  | sellerName | string | 卖方名称 | 某某公司 |
  | itemList | list | 订单的内容 必须包含(itemCode, itemName, itemQuantity, unit, unitPrice, itemAmount) | [{"itemCode": "A01", "itemName": "PC", "itemQuantity": "10", "unit": "台", "unitPrice": "10000.00", "itemAmount": "100000"}] |
  | comments | String | 备注(非必填) |  |

+ 返回样例：

```json
{
  "msg": "发票保存成功",
  "code": 0
}
```

### 5.3 添加合同

+ URL:
    + `/api/add-contract`

+ 参数：

  | 参数名 | 类型 | 解释 | 例 |
  | --- | --- | ---  | --- |
  | contractType | string | 用户自定的合同类型 | 框架合同 |
  | contractCode | string | 用户自定的合同编号  | 2021-05-03-000001 |
  | contractName | string | 合同名称  | 样品采购合同 |
  | party1Id | long | 甲方的企业ID(非必填) | 1234567890 |
  | party2Id | long | 乙方的企业ID(非必填) | 1234567890 |
  | party3Id | long | 丙方的企业ID(非必填) | 1234567890 |
  | party4Id | long | 丁方的企业ID(非必填) | 1234567890 |
  | party1Name | string | 甲方的企业名称 | 某某有限公司 |
  | party2Name | string | 乙方的企业名称 | 某某有限公司 |
  | party3Name | string | 丙方的企业名称(非必填) | 某某有限公司 |
  | party4Name | string | 丁方的企业名称(非必填) | 某某有限公司 |
  | contractDate | string | 签订日期 | 2021-05-02 |
  | expDate | string | 到期日期 | 2051-05-02 |
  | comments | String | 备注(非必填) |  |

+ 返回样例：

```json
{
  "msg": "合同保存成功",
  "code": 0
}
```

## 错误码

| 错误码 | 解释 |
| --- | --- |
| 1 | 未知错误 |
| 100 | 缺少参数 |
| 101 | 签名无效 |
| 102 | 没有登录 |
| 103 | 登录失败 |
| 104 | 用户账号已被锁定 |
| 105 | 没有设置用户当前的机构 |
| 106 | 当前用户没有该企业的权限 |
| 200 | 用户已经存在 |
| 201 | 企业已经存在 |
| 300 | 资产类型错误 |
