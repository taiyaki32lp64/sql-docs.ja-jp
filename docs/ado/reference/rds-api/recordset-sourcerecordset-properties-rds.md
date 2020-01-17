---
title: Recordset、SourceRecordset プロパティ (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- Recordset property [ADO]
ms.assetid: a29e3fb9-306d-497a-9a59-1856a914e5e9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0cca4735e65ce5d96d431fa455181de921e4474
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963570"
---
# <a name="recordset-sourcerecordset-properties-rds"></a>Recordset、SourceRecordset プロパティ (RDS)
示す、**レコード セット**カスタム ビジネス オブジェクトからオブジェクトが返されます。  
  
 **適用対象します。** [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.SourceRecordset = Recordset  
Recordset = DataControl.Recordset   
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
 *レコード セット*  
 オブジェクト変数を表す、 **Recordset**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 設定することができます、 **SourceRecordset**プロパティを[レコード セット](../../../ado/reference/ado-api/recordset-object-ado.md)カスタム ビジネス オブジェクトから返されます。  
  
 これらのプロパティをカスタム プロセスを使用してバインド プロセスを処理するために使用できます。 ラップされた行セットを受信した、**レコード セット**を直接操作できるように、 **Recordset**プロパティの設定などのアクションを実行、または反復処理に使用、**レコード セット**.  
  
 設定することができます、 **SourceRecordset**プロパティまたは読み取り、 **Recordset**スクリプト コードの実行時にプロパティ。  
  
 **SourceRecordset**とは異なり、書き込み専用のプロパティは、 **Recordset**プロパティは読み取り専用プロパティです。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [レコード セットと SourceRecordset プロパティの例 (VBScript)](../../../ado/reference/rds-api/recordset-and-sourcerecordset-properties-example-vbscript.md)   
 [CreateRecordset メソッド (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)   
 [クエリ メソッド (RDS)](../../../ado/reference/rds-api/query-method-rds.md)


