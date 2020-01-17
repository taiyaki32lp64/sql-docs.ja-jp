---
title: 現在のレコードとレコード セットのサイズ |Microsoft Docs
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
ms.assetid: e63ff331-8655-4be7-82c6-e6cd6cc9d16d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a01e17ea9c786a724e5869a28bf4d8927b58ac81
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925694"
---
# <a name="current-record-and-size-of-recordset"></a>レコードセットの現在のレコードとサイズ
このセクションのサンプルでは、カーソルの現在位置を検索する方法を説明します**レコード セット**で[レコード セットを返す JScript コードの例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)します。  
  
## <a name="current-record"></a>現在のレコード  
 データセット内の現在のレコードに対応のカーソルの位置によって示されるが、**レコード セット**オブジェクト。 ときに、 **Recordset**オブジェクトは、呼び出しの結果として、データ ソースから返される**Recordset.Open**、 **Command.Execute**、または**Connection.Execute** (含む**Connection.NamedCommand**と**Connection.StoredProcedure**)、最初のレコードの位置にカーソルを設定します。 サンプル データセットの最初の現在のレコードは「おじさん Bob の有機的なドライなし」の項目。  
  
## <a name="size-of-recordset"></a>レコード セットのサイズ  
 サイズを調べるには**Recordset**オブジェクトの値を取得、 **Recordset.RecordCount**プロパティ。 この値は内のレコードの数を示す長整数、 **Recordset**します。 データセットは、Microsoft SQL server OLEDB プロバイダーから返される、この値は返される行の数を示します。 読み取り、 **RecordCount**プロパティを閉じている**Recordset**エラーが発生します。  
  
 レコードの数を決定できない場合、プロパティの値は-1 です。  
  
 値、 **RecordCount**プロパティは、プロバイダーと使用するカーソルの種類の機能にも依存します。 順方向専用カーソルの場合は、値は-1 です。 静的またはキーセット カーソルでは、値は実際に返されるレコード数、 **Recordset**オブジェクト。 動的カーソルの場合、値は-1 またはデータ ソースによって、レコードの実際の数です。  
  
 サポートするカーソル**Recordcount**する必要があります作業困難ですが、そのために必要カーソルはサポートしていませんよりも多くのコンピューティング能力**Recordcount**します。 レコードの数を把握する必要がない場合異なるカーソルの種類を使用して可能性があります、アプリケーションのパフォーマンス向上、大規模なデータ セットを処理する必要がある場合に特にします。  
  
 場合によっては、プロバイダーまたはカーソルは判断できません、 **RecordCount**値、データ ソースからすべてのレコードを取得します。 正確なカウントを確実に呼び出す、 **Recordset**.**MoveLast**メソッドを呼び出す前に**Recordset.RecordCount**します。  
  
 サンプル**レコード セット**オブジェクトを使用して取得、 [JScript のコード例](../../../ado/guide/data/jscript-code-example-to-return-a-recordset.md)呼び出すので、順方向専用カーソルを使用して**RecordCount**オブジェクトで常には、結果では、-1。 呼び出すコード行を変更する場合、 **Recordset**.**開いている**メソッドでは、次の例で示すように、 **RecordCount**プロパティがフェッチされたレコードの実際の数を返します。  
  
```  
oRs.Open sSQL, sCnStr, adOpenStatic, adLockOptimistic, adCmdText   
```  
  
 これは静的カーソルを[Microsoft OLE DB Provider for SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md)サポート**RecordCount**します。 この例では、5 つのレコードと、それに伴って**RecordCount** 5 の値を生成する必要があります。  
  
 このセクションには、次のトピックが含まれています。  
  
 [レコードセットの境界](../../../ado/guide/data/boundaries-of-a-recordset.md)
