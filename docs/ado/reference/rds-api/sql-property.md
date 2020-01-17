---
title: SQL プロパティ |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
helpviewer_keywords:
- SQL property [RDS]
ms.assetid: e0dabf23-a159-4fe5-a962-3df544a21f5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f70eba6b5f53be7068708fdd8b139f0add10be90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963349"
---
# <a name="sql-property"></a>SQL プロパティ
取得するために使用するクエリ文字列を示します、 [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)します。  
  
 設定することができます、 **SQL**でデザイン時にプロパティ、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトのオブジェクトのタグ、または実行時にスクリプト コードです。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
Design time: <PARAM NAME="SQL" VALUE="QueryString">  
Run time: DataControl.SQL = "QueryString"  
```  
  
#### <a name="parameters"></a>パラメーター  
 *QueryString*  
 A**文字列**有効な SQL データの要求を表す値です。  
  
 *DataControl*  
 オブジェクト変数を表す、 **rds.DataControl**オブジェクト。  
  
## <a name="remarks"></a>コメント  
 一般に、これは、SQL ステートメント (データベース サーバーの言語を使用) など`"Select * from NewTitles"`します。 レコードを一致し、正確に更新されることを確認するには、更新可能なクエリはバイナリ長フィールドまたは計算フィールド以外のフィールドを含める必要があります。  
  
 **SQL**プロパティは、サーバー側のカスタム ビジネス オブジェクトは、クライアントのデータを取得する場合は省略可能です。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [SQL プロパティの例 (VBScript)](../../../ado/reference/rds-api/sql-property-example-vbscript.md)   
 [接続プロパティ (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)   
 [クエリ メソッド (RDS)](../../../ado/reference/rds-api/query-method-rds.md)   
 [Refresh メソッド (RDS)](../../../ado/reference/rds-api/refresh-method-rds.md)   
 [SubmitChanges メソッド (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


