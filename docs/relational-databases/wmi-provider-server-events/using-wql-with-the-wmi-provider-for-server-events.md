---
title: WMI Provider for Server Events と WQL の使用
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 57f7e07de49b2591e9ab0ef74603d674543282e9
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/06/2019
ms.locfileid: "73660490"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>WMI Provider for Server Events と WQL の使用
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  管理アプリケーションは WQL (WMI Query Language) ステートメントを実行することにより、WMI Provider for Server Events を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] イベントにアクセスすることができます。 WQL は、WMI 特有の拡張機能を複数持つ、構造化照会言語 (SQL) の単純化されたサブセットです。 WQL を使用した場合、アプリケーションは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンス、データベース、またはデータベース オブジェクト (現在サポートされているオブジェクトはキューのみ) に対してイベントの種類を取得します。 WMI Provider for Server Events は、データベーススコープまたはオブジェクトスコープのイベント通知の対象データベースで作成されたイベント通知、またはサーバースコープのイベント通知の**master**データベースにクエリを変換します。  
  
 たとえば、次の WQL クエリについて考えてみます。  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 このクエリから、WMI プロバイダーは、このイベント通知と同等のものをターゲット サーバー上に生成しようとします。  
  
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
  
 WQL クエリ (`FROM`) の `DDL_DATABASE_LEVEL_EVENTS` 句の引数には、イベント通知を作成できる有効なイベントを指定することができます。 `SELECT` 句および `WHERE` 句の引数は、イベントまたはその親イベントに関連付けられたイベント プロパティを指定することができます。 有効なイベントおよびイベントプロパティの一覧については、「[イベント通知 (データベースエンジン)](https://technet.microsoft.com/library/ms182602.aspx)」を参照してください。  
  
 次の WQL 構文は、WMI Provider for Server Events によって明示的にサポートされます。 追加の WQL 構文を指定することもできますが、このプロバイダーに特有ではないため、代わりに WMI ホスト サービスによって解析されます。 WMI Query Language の詳細については、Microsoft Developer Network (MSDN) の WQL のドキュメントを参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>引数  
 *event_property*  
 イベントのプロパティ。 例として、 **Posttime**、 **SPID**、および**loginが**あります。 「 [WMI Provider For Server Events のクラスとプロパティ](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md)」に記載されている各イベントを参照して、どのプロパティが保持されているかを判断します。 たとえば、DDL_DATABASE_LEVEL_EVENTS イベントには、 **DatabaseName**プロパティと**UserName**プロパティが保持されます。 また、親イベントから**SQLInstance**、 **login、** **posttime**、 **SPID**、および**ComputerName**プロパティも継承します。  
  
 **,** *...n*  
 *Event_property*をコンマで区切って複数回照会できることを示します。  
  
 \*  
 イベントに関連付けられたすべてのプロパティを照会することを指定します。  
  
 *event_type*  
 イベント通知を作成できるイベント。 使用できるイベントの一覧については、「 [WMI Provider For Server events のクラスとプロパティ](https://technet.microsoft.com/library/ms186449.aspx)」を参照してください。 イベントの*種類*名は、CREATE event notification を使用して手動でイベント通知を作成するときに指定できるのと同じ*event_type* | *event_group*に対応していることに注意してください。 イベントの*種類*の例としては、CREATE_TABLE、LOCK_DEADLOCK、DDL_USER_EVENTS、TRC_DATABASE などがあります。  
  
> [!NOTE]  
>  DDL に似た操作を実行する一部のシステム ストアド プロシージャもイベント通知を起動することができます。 イベント通知はテストして、実行されているシステム ストアド プロシージャに応答するかどうか、確認してください。 たとえば、CREATE TYPE ステートメントと**sp_addtype**ストアドプロシージャはどちらも、CREATE_TYPE イベントで作成されたイベント通知を起動します。 ただし、 **sp_rename**ストアドプロシージャでは、イベント通知は発生しません。 詳細については、「[DDL イベント](../../relational-databases/triggers/ddl-events.md)」を参照してください。  
  
 *where_condition*  
 *Event_property*名および論理演算子と比較演算子で構成される WHERE 句のクエリ述語です。 *Where_condition*によって、対応するイベント通知が対象のデータベースに登録されるスコープが決まります。 また、event_type のクエリを実行する特定のスキーマまたはオブジェクトを対象とするフィルターとしても機能し*ます。* 詳細については、このトピックで後述する「解説」を参照してください。  
  
 **DatabaseName**、 **SchemaName**、および**ObjectName**と共に使用できるのは、`=` のオペランドだけです。 その他の式は、これらのイベント プロパティと共に使用することはできません。  
  
## <a name="remarks"></a>Remarks  
 WMI Provider for Server Events 構文の*where_condition*によって、次のことが決定されます。  
  
-   プロバイダーが指定された*event_type*を取得しようとするスコープ。サーバーレベル、データベースレベル、またはオブジェクトレベル (現在サポートされている唯一のオブジェクトは queue) です。 最終的に、このスコープは対象データベースで作成されたイベント通知の種類を決定します。 このプロセスは、イベント通知登録と呼ばれます。  
  
-   データベース、スキーマ、オブジェクトのうちの適切な登録場所。  
  
 WMI Provider for Server Events は、bottom-up および first-fit アルゴリズムを使用して、基になる EVENT NOTIFICATION に対してできるだけ小さなスコープを生成します。 アルゴリズムにより、サーバーの内部的な利用状況、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと WMI ホスト プロセス間のネットワーク トラフィックが最小になるように試行されます。 プロバイダーは、FROM 句で指定された*event_type*と WHERE 句の条件を調べ、基になるイベント通知を最も狭いスコープで登録しようとします。 プロバイダーが最も狭いスコープで登録できない場合は、登録が正常に終了するまで、順次より高いスコープでの登録が試行されます。 最も高いスコープ (サーバーレベル) に到達して失敗した場合、エラーがコンシューマーに返されます。  
  
 たとえば、WHERE 句で DatabaseName = **'** AdventureWorks **'** が指定されている場合、プロバイダーは [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースにイベント通知を登録しようとします。 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースが存在し、呼び出し側クライアントが、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] のイベント通知を作成するために必要な権限を持っている場合、登録は正常に完了します。 それ以外の場合は、イベント通知をサーバー レベルで登録しようとします。 WMI クライアントが必要な権限を持っている場合、登録は正常に終了します。 ただし、このシナリオでは、[!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースが作成されるまで、イベントはクライアントに返されません。  
  
 また、 *where_condition*をフィルターとして使用して、特定のデータベース、スキーマ、またはオブジェクトに対してクエリをさらに制限することもできます。 たとえば、次の WQL クエリについて考えてみます。  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 登録プロセスの結果によっては、この WQL クエリは、データベース レベルまたはサーバー レベルのどちらかに登録されます。 ただし、サーバー レベルに登録された場合でも、プロバイダーは、`ALTER_TABLE` テーブルには適用されない `AdventureWorks.Sales.SalesOrderDetail` イベントを最終的にフィルターします。 つまり、プロバイダーは、この特定のテーブル上で発生した `ALTER_TABLE` イベントのプロパティのみを返します。  
  
 `DatabaseName='AW1'` OR `DatabaseName='AW2'` などの複合式が指定された場合、2 つの異なるイベント通知ではなく、サーバー スコープで 1 つのイベント通知の登録が試行されます。 呼び出し側クライアントが権限を持っている場合、登録は正常に終了します。  
  
 `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` がすべて `WHERE` 句で指定されている場合、スキーマ `X`内のオブジェクト `Z` に直接イベント通知を登録しようとします。 クライアントが権限を持っている場合、登録は正常に終了します。 現時点では、オブジェクトレベルのイベントはキューでのみサポートされており、QUEUE_ACTIVATION *event_type*に対してのみサポートされていることに注意してください。  
  
 ある特定のスコープでは、すべてのイベントを照会できるわけではないことに注意してください。 たとえば、Lock_Deadlock など、トレース イベント上の WQL クエリ、または TRC_LOCKS などのトレース イベント グループは、サーバー レベルでのみ登録できます。 同様に、CREATE_ENDPOINT イベントおよび DDL_ENDPOINT_EVENTS イベント グループも、サーバー レベルでのみ登録できます。 イベントを登録するための適切なスコープの詳細については、「[イベント通知のデザイン](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx)」を参照してください。 *Event_type*をサーバーレベルでしか登録できない WQL クエリを登録しようとすると、常にサーバーレベルで作成されます。 WMI クライアントが権限を持っている場合、登録は正常に終了します。 それ以外の場合は、クライアントにエラーが返されます。 ただし、WHERE 句は、イベントに対応するプロパティに基づいたサーバー レベル イベントに対するフィルターとして使用できる場合もあります。 たとえば、多くのトレースイベントには、WHERE 句でフィルターとして使用できる**DatabaseName**プロパティがあります。  
  
 サーバースコープのイベント通知は、 **master**データベースに作成され、 [server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md)カタログビューを使用してメタデータを照会できます。  
  
 データベーススコープまたはオブジェクトスコープのイベント通知は、指定されたデータベースに作成され、 [event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md)カタログビューを使用してメタデータを照会できます。 (カタログ ビューのプレフィックスには、対応するデータベース名を使用する必要があります)。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. サーバー スコープのイベントを照会する  
 次の WQL クエリは、`SERVER_MEMORY_CHANGE` のインスタンス上で発生する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] トレース イベントのイベント プロパティをすべて取得します。  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>b. データベース スコープのイベントを照会する  
 次の WQL クエリは、`AdventureWorks` データベース内で発生し、`DDL_DATABASE_LEVEL_EVENTS` イベント グループに存在するイベントの特定のイベント プロパティを取得します。  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. データベース スコープのイベントを照会し、スキーマおよびオブジェクトでフィルター処理を行う  
 次のクエリは、テーブル `ALTER_TABLE` 上で発生する `AdventureWorks.Sales.SalesOrderDetail` イベントのイベント プロパティを取得します。  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>参照  
 [WMI Provider For Server Events の概念](https://technet.microsoft.com/library/ms180560.aspx)   
 [イベント通知 (データベースエンジン)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
