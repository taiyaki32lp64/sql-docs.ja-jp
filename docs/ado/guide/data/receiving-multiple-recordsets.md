---
title: 複数のレコード セットの受信 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- receiving multiple Recordsets [ADO]
- Recordset object [ADO], receiving multiple Recordsets
ms.assetid: 2a7ad7a6-f00d-4355-b0b5-d0ab957b0566
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d6e649201b8bf23a1b696d574baea2f4b049e06
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924532"
---
# <a name="receiving-multiple-recordsets"></a>複数のレコードセットの受信
[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)複数取得できます**レコード セット**オブジェクトが複数の SQL ステートメントを含む 1 つのコマンドの 1 つ**Recordset**あたりの SQL ステートメント。 順序、 **Recordset**s には、コマンド テキスト内の SQL ステートメントの配置の順序が返されます。  
  
 Microsoft OLE DB Provider for SQL Server は、コマンドには、COMPUTE 句が含まれている場合も複数の結果セットと ADO を返します。 次の SQL ステートメントを含むコマンドが 2 つの結果を返すなど**レコード セット**オブジェクト: 1 つの行セット (*ProductID*、 *ProductName*、*UnitPrice*)、およびその他のテーブルのすべての製品の平均価格。  
  
```  
SELECT ProductID, ProductName, UnitPrice   
  FROM PRODUCTS   
  COMPUTE AVG(UnitPrice)  
```  
  
 使用することができます、 **Recordset.NextRecordset** 2 つのオブジェクトを列挙するメソッド。  
  
 詳細については、次を参照してください。 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)します。
