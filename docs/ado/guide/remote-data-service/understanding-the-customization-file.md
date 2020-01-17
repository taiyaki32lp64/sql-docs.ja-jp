---
title: カスタマイズ ファイルの概要 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- customization file in RDS [ADO]
ms.assetid: 136f74bf-8d86-4a41-be66-c86cbcf81548
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 81a73044c1ab413fb2b49286814f3e6b3951c6c9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921968"
---
# <a name="understanding-the-customization-file"></a>カスタマイズ ファイルの概要
カスタマイズ ファイルの各セクション ヘッダーは、角かっこで構成されます ( **[]** ) 型とパラメーターを格納します。 次の 4 つのセクションの種類は、リテラル文字列で示されます。**connect**、 **sql**、 **userlist**、または**logs**です。 パラメーターは、リテラル文字列、既定値、ユーザー指定の識別子では、または何もです。  
  
> [!IMPORTANT]
>  Windows 8 および Windows Server 2012 以降、RDS サーバー コンポーネントに含まれていない、Windows オペレーティング システム (Windows 8 を参照してくださいと[Windows Server 2012 の互換性クックブック](https://www.microsoft.com/download/details.aspx?id=27416)の詳細)。 RDS クライアント コンポーネントは、Windows の将来のバージョンで削除されます。 新規の開発作業ではこの機能を使用しないようにし、現在この機能を使用しているアプリケーションは修正することを検討してください。 RDS を使用するアプリケーションに移行する必要があります[WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)します。  
  
 そのため、各セクションでは、次のセクション ヘッダーのいずれかでマークされます。  
  
```console
  
[ connect default ] [ connect    
identifier   
] [ sql  default ] [ sql    
identifier   
] [ userlist    
identifier   
] [ logs ]  
  
```  
  
 セクション ヘッダーには、次の一部が含まれています。  
  
|要素|説明|  
|----------|-----------------|  
|**connect**|接続文字列を変更するリテラル文字列。|  
|**sql**|リテラル文字列をコマンド文字列を変更します。|  
|**userlist**|特定のユーザーのアクセス権を変更するリテラル文字列。|  
|**logs**|操作上のエラーを記録するログ ファイルを示すリテラル文字列。|  
|**default**|識別子のないを指定または検索された場合に使用されるリテラル文字列。|  
|*identifier*|文字列に一致する文字列、**接続**または**コマンド**文字列。<br /><br /> セクションを使用してこのセクションのヘッダーが含まれている場合**connect**接続文字列で、識別子の文字列があるとします。<br />セクションを使用してこのセクションのヘッダーが含まれている場合**sql**コマンド文字列内に識別子の文字列があるとします。<br />セクションを使用してこのセクションのヘッダーが含まれている場合**userlist**識別子文字列と一致して、**connect**セクションの識別子。|  
  
 **DataFactory**クライアント パラメーターを渡して、ハンドラーが呼び出されます。 ハンドラーは、該当するセクション ヘッダー内の識別子に一致するクライアント パラメーターで全体の文字列を検索します。 一致が見つかった場合、そのセクションの内容は、クライアント パラメーターに適用されます。  
  
 特定のセクションは、次の状況で使用されます。  
  
-   A**接続**セクションを使用して、クライアントの値の部分文字列のキーワードを接続する場合は"**データ ソース =** _値_"と一致する、**接続**セクションの識別子です。 
  
-   **Sql** セクションには、クライアントのコマンド文字列に一致する文字列が含まれている場合、使用、 **sql** セクションの識別子。  
  
-   **connect**または**sql**既定パラメーターを持つセクションは、一致する識別子が存在しない場合に使用します。  
  
-   **userlist** セクションは場合、使用、 **userlist** 識別子と一致するセクション、**connect** セクションの識別子。 内容、一致がある場合、 **userlist** セクションは、制約を受ける接続に適用されます、**connect** セクションです。  
  
-   接続またはコマンド文字列内の文字列がいずれかで識別子と一致しない場合**connect** または**sql** セクションのヘッダー、およびがない**connect** または**sql** 変更せずに、クライアントの文字列を使用し、既定のパラメーターを持つヘッダーをセクションです。  
  
-   **logs** セクションは、使用されるたびに、 **DataFactory** の操作ができます。  
  
## <a name="see-also"></a>参照  
 [カスタマイズ ファイル Connect セクション](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [カスタマイズ ファイル Logs セクション](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [カスタマイズ ファイル SQL セクション](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [カスタマイズ ファイル UserList セクション](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory のカスタマイズ](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必要なクライアント設定](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [独自のカスタム ハンドラーの記述](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

