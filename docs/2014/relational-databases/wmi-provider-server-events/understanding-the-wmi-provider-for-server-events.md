---
title: WMI Provider for Server Events の理解 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 2deedb64e5c8995524978a19b02110a068bde08d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68195815"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>WMI Provider for Server Events について
  WMI Provider for Server Events を使用すれば、Windows Management Instrumentation (WMI) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のイベントを監視できます。 このプロバイダーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を WMI マネージド オブジェクトに変えることによって機能します。 このプロバイダーを使用することにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でイベント通知を生成できるイベントはすべて、WMI で利用できるようになります。 さらに、WMI と連動する管理アプリケーションとして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがそのイベントに応答できるので、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで対応できるイベントのスコープが以前のリリースより広くなります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントなどの管理アプリケーションは、WQL (WMI Query Language) ステートメントを実行することで WMI Provider for Server Events を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントにアクセスすることができます。 WQL は、WMI 特有の拡張機能を複数持つ、構造化照会言語 (SQL) の単純化されたサブセットです。 WQL を使用した場合、アプリケーションは特定のデータベースまたはデータベース オブジェクトに対してイベントの種類を取得します。 WMI Provider for Server Events は、クエリをイベント通知に変換し、対象データベース内のイベント通知を効率的に作成します。 イベント通知の動作の詳細については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[WMI Provider for Server Events の概念](https://technet.microsoft.com/library/ms180560.aspx)します。 クエリを実行できるイベントは、「 [WMI Provider for Server Events のクラスとプロパティ](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)します。  
  
 メッセージを送信するイベント通知をトリガーするイベントの発生時に、メッセージが定義済みの対象サービスには**msdb**という**SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**. サービスがイベントを定義済みでキューに配置**msdb**という**WMIEventProviderNotificationQueue**します。 (サービスもキューも、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に最初に接続する際にプロバイダーによって動的に作成されます)。プロバイダーは、このキューからイベント データを読み取り、それをマネージド オブジェクト フォーマット (MOF) に変換してからアプリケーションに返します。 次の図に、このプロセスを示します。  
  
 ![WMI Provider for Server Events のフロー ダイアグラム](../../../2014/database-engine/dev-guide/media/wmi-provider-functional-spec.gif "WMI Provider for Server Events のフロー図")  
  
 たとえば、次の WQL クエリについて考えてみます。  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 このクエリに応答して、WMI Provider for Server Events は、対象データベース内に同等のイベント通知を作成します。  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 この例では、`SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` は、プレフィックス `SQLWEP_` と GUID から構成される [!INCLUDE[tsql](../../includes/tsql-md.md)] 識別子です。 `SQLWEP` は、各識別子に対して新しい GUID を作成します。 値`A7E5521A-1CA6-4741-865D-826F804E5135`で、`TO SERVICE`句内の broker インスタンスを識別する GUID では、 **msdb**データベース。  
  
 WQL を使用する方法の詳細については、次を参照してください。 [WMI Provider for Server Events と WQL の使用](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)します。  
  
 管理アプリケーションは、プロバイダーによって定義された WMI 名前空間に接続することで、WMI Provider for Server Events を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにダイレクトします。 Windows WMI サービスは、この名前空間をプロバイダー DLL である Sqlwep.dll にマップし、これをメモリに読み込みます。 各インスタンスについてプロバイダーがサーバー イベント用 WMI 名前空間を管理[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]、形式は次です: \\ \\.\\*ルート*\Microsoft\SqlServer\ServerEvents\\*instance_name*ここで、 *instance_name*既定では MSSQLSERVER です。 インスタンスの WMI 名前空間に接続する方法についての詳細は[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[WMI Provider for Server Events と WQL の使用](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)します。  
  
 プロバイダー DLL である Sqlwep.dll は、サーバー上にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの数にかかわらず、サーバーのオペレーティング システムの WMI ホスト サービスに一度だけ読み込まれます。  
  
 例については、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] for Server Events, WMI プロバイダーを使用するエージェント管理アプリケーションを参照してください[サンプル。サーバー イベント用 WMI プロバイダーを使用して SQL Server エージェント警告の作成](https://technet.microsoft.com/library/ms186385.aspx)です。 マネージ コードでサーバー イベント用 WMI プロバイダーを使用する管理アプリケーションの例は、次を参照してください。[サンプル。WMI イベント プロバイダーを使用してマネージ コード](https://technet.microsoft.com/library/ms179315.aspx)します。 WMI の詳細についての詳細についてはまた、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Server Events の概念](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
