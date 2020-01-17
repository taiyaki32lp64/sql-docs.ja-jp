---
title: WMI Provider for Server Events について
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
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
ms.openlocfilehash: 63cc23d19a6eeb5f3a44cd0bbf62d9bcd87ace0d
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660515"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>WMI Provider for Server Events について
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  WMI Provider for Server Events を使用すれば、Windows Management Instrumentation (WMI) を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のイベントを監視できます。 このプロバイダーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を WMI マネージド オブジェクトに変えることによって機能します。 このプロバイダーを使用することにより、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でイベント通知を生成できるイベントはすべて、WMI で利用できるようになります。 さらに、WMI と連動する管理アプリケーションとして、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントがそのイベントに応答できるので、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントで対応できるイベントのスコープが以前のリリースより広くなります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントなどの管理アプリケーションは、WQL (WMI Query Language) ステートメントを実行することで WMI Provider for Server Events を使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントにアクセスすることができます。 WQL は、WMI 特有の拡張機能を複数持つ、構造化照会言語 (SQL) の単純化されたサブセットです。 WQL を使用した場合、アプリケーションは特定のデータベースまたはデータベース オブジェクトに対してイベントの種類を取得します。 WMI Provider for Server Events は、クエリをイベント通知に変換し、対象データベース内のイベント通知を効率的に作成します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でのイベント通知の動作の詳細については、「 [WMI Provider For Server Events の概念](https://technet.microsoft.com/library/ms180560.aspx)」を参照してください。 クエリ可能なイベントは、「 [WMI Provider For Server events のクラスとプロパティ](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)」に記載されています。  
  
 イベント通知をトリガーしてメッセージを送信するイベントが発生すると、メッセージは、 **SQL/notification/Processの Eventprovidernotification/** v1.0 という名前の**msdb**内の定義済みの対象サービスに送られます。 サービスは、このイベントを、" **wmi**" という名前の**msdb**内の定義済みキューに配置します。 (サービスとキューの両方が、最初に [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に接続するときにプロバイダーによって動的に作成されます)。次に、プロバイダーはこのキューからイベントデータを読み取り、それをマネージオブジェクト形式 (MOF) に変換してからアプリケーションに返します。 次の図に、このプロセスを示します。  
  
 ![WMI Provider for Server Events のフロー図](../../relational-databases/wmi-provider-server-events/media/wmi-provider-functional-spec.gif "WMI Provider for Server Events のフロー図")  
  
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
  
 この例では、`SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` は、プレフィックス [!INCLUDE[tsql](../../includes/tsql-md.md)] と GUID から構成される `SQLWEP_` 識別子です。 `SQLWEP` は、各識別子に対して新しい GUID を作成します。 `TO SERVICE` 句の `A7E5521A-1CA6-4741-865D-826F804E5135` 値は、 **msdb**データベース内のブローカーインスタンスを識別する GUID です。  
  
 WQL の使用方法の詳細については、「 [WMI Provider For Server Events での wql の使用](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)」を参照してください。  
  
 管理アプリケーションは、プロバイダーによって定義された WMI 名前空間に接続することで、WMI Provider for Server Events を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにダイレクトします。 Windows WMI サービスは、この名前空間をプロバイダー DLL である Sqlwep.dll にマップし、これをメモリに読み込みます。 プロバイダーは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各インスタンスについて、サーバーイベントの WMI 名前空間を管理します。形式は \\\\です。\\*ルート*\Microsoft\SqlServer\ServerEvents\\*instance_name*、 *instance_name*既定値は MSSQLSERVER です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスの WMI 名前空間に接続する方法の詳細については、「 [Wmi Provider For Server Events での WQL の使用](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx)」を参照してください。  
  
 プロバイダー DLL である Sqlwep.dll は、サーバー上にある [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの数にかかわらず、サーバーのオペレーティング システムの WMI ホスト サービスに一度だけ読み込まれます。  
  
 WMI Provider for server Events を使用する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント管理アプリケーションの例については、「[サンプル: Wmi provider For Server Events を使用した SQL Server エージェントアラートの作成](https://technet.microsoft.com/library/ms186385.aspx)」を参照してください。 WMI Provider for Server Events をマネージコードで使用する管理アプリケーションの例については、「[サンプル: マネージコードでの Wmi イベントプロバイダーの使用](https://technet.microsoft.com/library/ms179315.aspx)」を参照してください。 詳細については、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK の WMI に関する情報も参照してください。  
  
## <a name="see-also"></a>参照  
 [WMI Provider for Server Events の概念](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
