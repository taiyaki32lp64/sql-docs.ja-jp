---
title: 必須のクライアント設定 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdb99cb3d792900f48ceb69c25c7ae720c339683
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922293"
---
# <a name="required-client-settings"></a>必要なクライアントの設定
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 カスタムを使用する次の設定を指定**DataFactory**ハンドラー。  
  
-   指定"プロバイダー = MS リモート"で、[接続オブジェクト (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)オブジェクト[プロバイダー プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)プロパティまたは**接続**接続文字列をオブジェクト"**プロバイダー**="キーワード。  
  
-   設定、 [CursorLocation プロパティ (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)プロパティを**adUseClient**します。  
  
-   使用するハンドラーの名前を指定、 [DataControl オブジェクト (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)オブジェクトの**ハンドラー**プロパティ、または[レコード セット オブジェクト (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)オブジェクトの接続文字列"**ハンドラー**="キーワード。 (でハンドラーを設定することはできません、**接続**オブジェクトの接続文字列です)。  
  
 RDS という名前のサーバーで、既定のハンドラーを提供する**MSDFMAP します。ハンドラー**します。 (既定のカスタマイズ ファイルの MSDFMAP を名前です。INI。)  
  
 **例**  
  
 以下のセクションを前提としています。 **MSDFMAP します。INI** AdvWorks、データ ソース名は既に定義されているとします。  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 Visual Basic では、次のコード スニペットが書き込まれます。  
  
## <a name="rdsdatacontrol-version"></a>RDS.DataControl バージョン  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>レコード セットのバージョン  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 いずれかを指定、[ハンドラー プロパティ (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)プロパティまたはキーワード;、[プロバイダー プロパティ (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)プロパティまたはキーワード; および*CustomerById*と*CustomerDatabase*識別子。 開き、 **Recordset**オブジェクト  
  
 rs。"CustomerById(4)"開く"ハンドラー MSDFMAP を = です。_ (&)、ハンドラーです。"  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>関連項目  
 [カスタマイズ ファイル Connect セクション](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [カスタマイズ ファイル SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [カスタマイズ ファイル UserList セクション](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要なクライアント設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [カスタマイズ ファイルの概要](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

