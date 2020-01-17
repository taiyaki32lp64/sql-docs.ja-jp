---
title: データを確認するためのレコード セットのサンプル |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record location [ADO]
- current record [ADO]
ms.assetid: e770e626-68b1-4ddf-a217-d7b30311e2ee
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1882c5298d92e17a7ddaa165288fddfab7fdb02b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924302"
---
# <a name="sample-recordset-for-examining-data"></a>データを確認するためのサンプルのレコードセット
最初に、見て、**レコード セット**Microsoft SQL server ベースの Northwind サンプル データに対して実行される次の SQL クエリを使用して返されるオブジェクトします。  
  
```  
SELECT ProductID,ProductName,UnitPrice   
FROM Products   
WHERE CategoryID = 7    
```  
  
 結果として得られる**Recordset**オブジェクトには、次の表に示すように、データベース内のすべての生成が含まれています。  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|7|おじさん Bob の有機的な乾燥なし|30.0000|  
|14|階層|23.2500|  
|28|Rssle ザワークラウト|45.6000|  
|51|りんご|53.0000|  
|74|Longlife 階層|10.0000|  
  
 自分でこれらの結果を取得する場合は、次の JScript の例を試してください。  
  
-   [レコード セットを返す JScript の例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)
