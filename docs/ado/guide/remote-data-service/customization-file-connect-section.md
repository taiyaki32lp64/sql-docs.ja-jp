---
title: カスタマイズ ファイルの Connect セクション |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1de3710590cf49de30ff8e79a6ff829b124c42dd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922804"
---
# <a name="customization-file-connect-section"></a>カスタマイズ ファイルの Connect セクション
ハンドラーの既定の動作では、すべての接続を拒否します。 **接続**セクションでは、その動作の例外を指定します。 たとえば、すべての場合、**接続**セクションが存在しない場合、または空の場合、既定で接続を確立できませんでした。  
  
 **接続**セクションに含めることができます。  
  
-   既定値を指定する既定のアクセス エントリは、この接続で許可される操作を読み書きします。 セクション内に既定のアクセス エントリがない場合は、セクションは無視されます。  
  
-   クライアントの接続文字列を置換する新しい接続文字列。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
## <a name="syntax"></a>構文  
 形式は、既定のアクセス エントリです。  
  
```console
  
Access=  
accessRight  
  
```  
  
 形式は、接続文字列の置換エントリです。  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>コメント  
  
|要素|説明|  
|----------|-----------------|  
|**Connect**|これを示すリテラル文字列は、接続文字列のエントリです。|  
|**_ConnectionString_**|全体のクライアントの接続文字列を置換する文字列。|  
|**アクセス**|これを示すリテラル文字列は、アクセス エントリです。|  
|**_アクセス権_**|次のアクセス権のいずれか:<br /><br /> -   **NoAccess** -ユーザーがデータ ソースにアクセスできません。<br />-   **読み取り専用**-ユーザーがデータ ソースを読み取ることができます。<br />-   **ReadWrite** -ユーザーの読み取りまたはデータ ソースへの書き込みができます。|  
  
 (影響-既定のハンドラーの動作を無効にする) で任意の接続を許可する場合でアクセス エントリを設定、**接続既定**セクションを`Access=ReadWrite`、および削除またはコメント アウト、他の**を接続**_識別子_セクション。  
  
## <a name="see-also"></a>関連項目  
 [カスタマイズ ファイル Logs セクション](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [カスタマイズ ファイル SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [カスタマイズ ファイル UserList セクション](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要なクライアント設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [カスタマイズ ファイルの概要](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [独自のカスタム ハンドラーの記述](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



