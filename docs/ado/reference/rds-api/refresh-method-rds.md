---
title: Refresh メソッド (RDS) |Microsoft Docs
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
apitype: COM
f1_keywords:
- Refresh
- RDS.DataControl::Refresh
- DataControl::Refresh
helpviewer_keywords:
- Refresh method [RDS]
ms.assetid: c90a8050-0ff4-4c83-9925-261f2f2ccfe9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb7cb94edab6b5422c315b71c2900662f85aa1e2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67963509"
---
# <a name="refresh-method-rds"></a>Refresh メソッド (RDS)
指定されたデータ ソースを再クエリ、 [Connect](../../../ado/reference/rds-api/connect-property-rds.md)プロパティと、クエリの結果を更新します。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
  
```  
  
DataControl.Refresh  
```  
  
#### <a name="parameters"></a>パラメーター  
 *DataControl*  
 オブジェクト変数を表す、 [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクト。  
  
## <a name="remarks"></a>コメント  
 設定する必要があります、 [Connect](../../../ado/reference/rds-api/connect-property-rds.md)、 [Server](../../../ado/reference/rds-api/server-property-rds.md)、および[SQL](../../../ado/reference/rds-api/sql-property.md)プロパティを使用する前に、**更新**メソッド。 関連付けられているフォーム上のすべてのデータ バインド コントロールを**rds.DataControl**オブジェクトが新しいレコード セットに反映されます。 既存の[Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトがリリースされ、未保存の変更は破棄されます。 **更新**メソッドが現在のレコードに自動最初のレコードにで行います。  
  
 呼び出すことをお勧め、**更新**メソッド定期的に使用する場合のデータ。 データを取得してしばらくの間、クライアント コンピューターのままに古くなる可能性があります。 行った変更が失敗する、他のユーザーがレコードを変更したし、する前に変更を送信するために可能性があります。  
  
## <a name="applies-to"></a>適用対象  
 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)  
  
## <a name="see-also"></a>関連項目  
 [Refresh メソッドの例 (VB)](../../../ado/reference/ado-api/refresh-method-example-vb.md)   
 [Refresh メソッドの例 (VBScript)](../../../ado/reference/rds-api/refresh-method-example-vbscript.md)   
 [アドレス帳のコマンド ボタン](../../../ado/guide/remote-data-service/address-book-command-buttons.md)   
 [CancelUpdate メソッド (RDS)](../../../ado/reference/rds-api/cancelupdate-method-rds.md)   
 [Refresh メソッド (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [SubmitChanges メソッド (RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


