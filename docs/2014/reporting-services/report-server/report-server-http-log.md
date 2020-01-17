---
title: レポート サーバーの HTTP ログ |Microsoft ドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ca3437315803ff8435640bf58219fe93f96e242a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66103395"
---
# <a name="report-server-http-log"></a>レポート サーバーの HTTP ログ
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] レポート サーバーの HTTP ログ ファイルには、レポート サーバーによって処理された HTTP 要求および HTTP 応答がすべて記録されます。 要求のオーバーフローやタイムアウト エラーは、レポート サーバーに到達しないため、ログ ファイルには記録されません。  
  
 HTTP ログは既定では有効になっていません。 HTTP ログ記録を有効にするには、 **ReportingServicesService.exe.config**インストールでこの機能を使用する構成ファイル。  
  
## <a name="viewing-log-information"></a>ログ情報の表示  
 ログは、ASCII テキスト ファイルです。 任意のテキスト エディターでファイルを閲覧できます。 レポート サーバーの HTTP ログ ファイルは、IIS における W3C 拡張ログ ファイルに相当し、同様のフィールドが使用されています。そのため、既存の IIS ログ ファイル ビューアーを使用して、レポート サーバーの HTTP ログ ファイルを閲覧することもできます。 次の表に、HTTP ログ ファイルの補足情報を示します。  
  
|||  
|-|-|  
|**[ファイル名]**|既定では、ログ ファイル名は次のとおりです。<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> ReportingServicesService.exe.config ファイルで HttpTraceFileName 属性を変更することにより、ファイル名のプレフィックスをカスタマイズできます。 タイムスタンプには、協定世界時 (UTC) が使用されます。|  
|**ファイルの場所**|ファイルは、次の場所に書き込まれます。<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**ファイル形式**|このファイルは EN-US 形式です。 ASCII テキスト ファイルです。|  
|**ファイルの作成と保存**|HTTP ログは、構成ファイルでログ機能を有効にし、サービスを再開した後、レポート サーバーによって HTTP 要求が処理されて初めて作成されます。 設定を構成したにもかかわらず、ログ ファイルが確認できない場合は、レポートを開くか、レポート サーバー アプリケーション (レポート マネージャーなど) を起動して、HTTP 要求を生成すると、ログ ファイルが作成されます。<br /><br /> ログ ファイルの新しいインスタンスは、各サービスが再開され、その後、HTTP 要求がレポート サーバーに送信されると作成されます。<br /><br /> 既定では、トレース ログのサイズの上限は 32 MB であり、14 日後に削除されます。|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>レポート サーバーの HTTP ログの構成設定  
 レポート サーバーの HTTP ログを構成するには、メモ帳を使用して変更する、 **ReportingServicesService.exe.config**ファイル。 構成ファイルは、\Program Files\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin フォルダーに格納されています。  
  
 HTTP サーバーを有効にするには、`http:4` を、ReportingServicesService.exe.config ファイルの RStrace セクションに追加します。 その他の HTTP ログ ファイル エントリはすべてオプションです。 次の例には、RStrace セクションに上書きする形でセクション全体を貼り付けて、不要な設定を削除するだけで済むように、すべての設定が含まれています。  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>ログ ファイル フィールド  
 次の表は、ログで利用できるフィールドの一覧です。 ログに含めるフィールドは、`HTTPTraceSwitches` 構成設定で指定できます。 **既定**列を指定、フィールドを追加するどうか、ログ ファイルに自動的に指定しない場合`HTTPTraceSwitches`します。  
  
|フィールド|説明|既定|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|この値は省略可能です。 既定値は ReportServerServiceHTTP_ です。 別のファイル名前付け規則 (ログ ファイルを一元管理する場合はサーバー名など) を使用する場合は、異なる値を指定できます。|はい|  
|HTTPTraceSwitches|この値は省略可能です。 指定した場合、ログ ファイルに使用するフィールドをコンマ区切り形式で構成できます。|いいえ|  
|date|アクティビティが発生した日付。|いいえ|  
|Time|アクティビティが発生した時刻。|いいえ|  
|ClientIp|レポート サーバーにアクセスしているクライアントの IP アドレス。|はい|  
|UserName|レポート サーバーにアクセスしたユーザー名。|いいえ|  
|ServerPort|接続に使用されたポート番号。|いいえ|  
|ホスト|ホスト ヘッダーの内容。|いいえ|  
|方法|クライアントから呼び出されたアクションまたは SOAP メソッド。|はい|  
|UriStem|アクセスされたリソース。|はい|  
|UriQuery|リソースへのアクセスに使用されたクエリ。|いいえ|  
|ProtocolStatus|HTTP 状態コード。|はい|  
|BytesReceived|サーバーが受信したバイト数。|いいえ|  
|TimeTaken|HTTP.SYS が要求データを返してから、サーバーが最後の送信を完了するまでのミリ秒単位の時間 (ネットワークの伝送時間を除く)。|いいえ|  
|ProtocolVersion|クライアントが使用するプロトコル バージョン。|いいえ|  
|UserAgent|クライアントが使用しているブラウザーの種類。|いいえ|  
|CookieReceived|サーバーが受信したクッキーの内容。|いいえ|  
|CookieSent|サーバーによって送信されたクッキーの内容。|いいえ|  
|Referrer|クライアントが直前に訪問したサイト。|いいえ|  
  
## <a name="see-also"></a>関連項目  
 [Report Server Service Trace Log](report-server-service-trace-log.md)   
 [Reporting Services のログ ファイルとソース](../report-server/reporting-services-log-files-and-sources.md)   
 [エラーとイベントのリファレンス (Reporting Services)](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
