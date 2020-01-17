---
title: CREATE ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: b70035a1fc54d4b59978a3256b2ed3040ba4e8f9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006507"
---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md )]

  新しいルートを現在のデータベース用のルーティング テーブルに追加します。 送信メッセージについては、[!INCLUDE[ssSB](../../includes/sssb-md.md)] がローカル データベース内のルーティング テーブルを調べてルーティングを決定します。 転送されるメッセージなど、別のインスタンスで発生するメッセージ交換でのメッセージについては、[!INCLUDE[ssSB](../../includes/sssb-md.md)] が **msdb** 内のルートを調べます。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>引数  
 *route_name*  
 作成するルートの名前です。 新しいルートが現在のデータベースで作成され、AUTHORIZATION 句で指定されるプリンシパルによって所有されます。 サーバー名、データベース名、スキーマ名は指定できません。 *route_name* は有効な **sysname** とする必要があります。  
  
 AUTHORIZATION *owner_name*  
 ルートの所有者を、指定したデータベース ユーザーまたはロールに設定します。 現在のユーザーが **db_owner** 固定データベース ロールまたは **sysadmin** 固定サーバー ロールのメンバーである場合、*owner_name* には、任意の有効なユーザー名またはロール名を指定できます。 それ以外の場合、*owner_name* には、現在のユーザーの名前、現在のユーザーが IMPERSONATE 権限を持つユーザーの名前、または現在のユーザーが属するロールの名前を指定する必要があります。 この句を省略すると、ルートは現在のユーザーに属します。  
  
 WITH  
 作成されるルートを定義するための句を、WITH の後に指定します。  
  
 SERVICE_NAME = **'** _service\_name_ **'**  
 このルートが示すリモート サービスの名前を指定します。 *service_name* はリモート サービスで使用される名前と正確に一致する必要があります。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は *service_name* をバイト単位で照合します。 つまり、この比較では大文字と小文字が区別され、現在の照合順序は考慮されません。 SERVICE_NAME が省略されると、このルートはすべてのサービス名と照合されることになりますが、SERVICE_NAME が指定されたルートより照合の優先度が下がります。 **'SQL/ServiceBroker/BrokerConfiguration'** というサービス名を持つルートは、Broker Configuration Notice サービスへのルートです。 このサービスへのルートは、ブローカー インスタンスを指定できない場合があります。  
  
 BROKER_INSTANCE = **'** _broker\_instance\_identifier_ **'**  
 発信先サービスをホストするデータベースを指定します。 *broker_instance_identifier* パラメーターは、リモート データベースのブローカー インスタンス識別子である必要があります。この識別子は選択したデータベースで、次のクエリを実行して取得できます。  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 BROKER_INSTANCE 句を省略すると、このルートはすべてのブローカー インスタンスと照合されます。 ブローカー インスタンスを指定しないメッセージ交換では、すべてのブローカー インスタンスと照合されるルートは、明示的なブローカー インスタンスを持つルートよりも照合の優先度が高くなります。 ブローカー インスタンスを指定するメッセージ交換では、ブローカー インスタンスを持つルートの方が、すべてのブローカー インスタンスと照合されるルートより優先度が高くなります。  
  
 LIFETIME **=** _route\_lifetime_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がルーティング テーブルにルートを保持する時間を秒単位で指定します。 有効期間が終了するとルートは期限切れとなり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、新しいメッセージ交換用のルートを選択するときに、そのルートは考慮されなくなります。 この句を省略した場合、*route_lifetime* は NULL になり、ルートの有効期限が切れることはありません。  
  
 ADDRESS **='** _next\_hop\_address_ **'**  
SQL Database マネージド インスタンスの場合、`ADDRESS` はローカルである必要があります。 

このルート用のネットワーク アドレスを指定します。 *next_hop_address* の次の形式で TCP/IP アドレスを指定します。  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** _port\_number_  
  
 指定した *port_number* は、指定したコンピューターにおける [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの [!INCLUDE[ssSB](../../includes/sssb-md.md)] エンドポイント用のポート番号と一致する必要があります。 これは選択したデータベースで次のクエリを実行することにより取得できます。  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 ミラー化されたデータベースでサービスがホストされる場合、ミラー化されたデータベースをホストする別のインスタンスに対して、MIRROR_ADDRESS を指定する必要もあります。 それ以外の場合は、このルートはミラーに対してフェールオーバーされません。  
  
 ルートの *next_hop_address* が **'LOCAL'** になっている場合、メッセージは現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のサービスに配信されます。  
  
 ルートの *next_hop_address* が **'TRANSPORT'** になっている場合、ネットワーク アドレスは、サービス名の中にあるネットワーク アドレスに基づいて決まります。 **'TRANSPORT'** を指定するルートは、サービス名やブローカー インスタンスを指定できない場合があります。  
  
 MIRROR_ADDRESS **='** _next\_hop\_mirror\_address_ **'**  
 *next_hop_address* でホストされているミラー化されたデータベースを 1 つ含んでいる、ミラー化されたデータベースのネットワーク アドレスを指定します。 *next_hop_mirror_address* は、次の形式で TCP/IP アドレスを指定します。  
  
 **TCP://** { *dns_name* | *netbios_name* | *ip_address* } **:** *port_number*  
  
 指定した *port_number* は、指定したコンピューターにおける [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの [!INCLUDE[ssSB](../../includes/sssb-md.md)] エンドポイント用のポート番号と一致する必要があります。 これは選択したデータベースで次のクエリを実行することにより取得できます。  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 MIRROR_ADDRESS が指定されている場合、ルートには SERVICE_NAME 句と BROKER_INSTANCE 句を指定する必要があります。 *next_hop_address* に **'LOCAL'** または **'TRANSPORT'** を指定するルートでは、ミラー アドレスが指定されない場合があります。  
  
## <a name="remarks"></a>Remarks  
 ルートを格納するルーティング テーブルは、**sys.routes** カタログ ビューを介して読み取ることができるメタデータ テーブルです。 このカタログ ビューを更新できるのは、CREATE ROUTE、ALTER ROUTE、および DROP ROUTE ステートメントだけです。  
  
 既定では、各ユーザー データベースにあるルーティング テーブルには 1 つのルートが含まれています。 このルートには **AutoCreatedLocal** という名前が付いています。 ルートは *next_hop_address* に **'LOCAL'** を指定し、任意のサービス名およびブローカー インスタンス識別子と一致します。  
  
 ルートが *next_hop_address* に **'TRANSPORT'** を指定した場合、ネットワーク アドレスはサービスの名前に基づいて決定されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*next_hop_address* のネットワーク アドレスが有効な形式であれば、このネットワーク アドレスで始まるサービス名が適切に処理されます。  
  
 ルーティング テーブルには、同じサービス、ネットワーク アドレス、ブローカー インスタンス識別子を指定する、ルートをいくつでも含めることができます。 このような場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] でルートを選択するときには、メッセージ交換で指定された情報とルーティング テーブル内の情報を照合して、最も正確に一致する情報を取得するためのプロシージャが使用されます。  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] では、ルーティング テーブルから期限の切れたルートは削除されません。 期限の切れたルートは、ALTER ROUTE ステートメントを使用してアクティブにすることができます。  
  
 ルートは一時オブジェクトとして指定できません。 **#** で始まるルート名は許可されますが、パーマネント オブジェクトになります。  
  
## <a name="permissions"></a>アクセス許可  
 ルートを作成する権限は、既定では **db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバー、および **sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. DNS 名を使用して TCP/IP ルートを作成する  
 次の例では、サービス `//Adventure-Works.com/Expenses` へのルートを作成します。 このルートでは、このサービスへのメッセージが、TCP 経由で DNS 名 `1234` に対応するホスト上のポート `www.Adventure-Works.com` に伝達されるように指定します。 ターゲット サーバーにメッセージが到着すると、一意識別子 `D8D4D268-00A3-4C62-8F91-634B89C1E315` で指定されるブローカー インスタンスにメッセージが配信されます。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. NetBIOS 名を使用して TCP/IP ルートを作成する  
 次の例では、サービス `//Adventure-Works.com/Expenses` へのルートを作成します。 このルートでは、このサービスへのメッセージが、TCP 経由で NetBIOS 名 `1234` に対応するホスト上のポート `SERVER02` へ伝達されるように指定します。 対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にメッセージが到着すると、一意識別子 `D8D4D268-00A3-4C62-8F91-634B89C1E315` で指定されるデータベース インスタンスにメッセージが配信されます。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. IP アドレスを使用して TCP/IP ルートを作成する  
 次の例では、サービス `//Adventure-Works.com/Expenses` へのルートを作成します。 このルートでは、このサービスへのメッセージが、TCP 経由で IP アドレス `1234` にあるホスト上のポート `192.168.10.2` へ伝達されるように指定します。 対象の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] にメッセージが到着すると、一意識別子 `D8D4D268-00A3-4C62-8F91-634B89C1E315` で指定されるブローカー インスタンスにメッセージが配信されます。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. 転送ブローカーへのルートを作成する  
 次の例では、サーバー `dispatch.Adventure-Works.com` の転送ブローカーへのルートを作成します。 サービス名とブローカー インスタンス識別子が両方とも指定されていないため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、他のルートが定義されていないサービスに対してこのルートが使用されます。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. ローカル サービスへのルートを作成する  
 次の例では、ルートと同じインスタンスにあるサービス `//Adventure-Works.com/LogRequests` へのルートを作成します。  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. 有効期間が指定されたルートを作成する  
 次の例では、サービス `//Adventure-Works.com/Expenses` へのルートを作成します。 ルートの有効期間は、`259200` 秒、つまり 72 時間です。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. ミラー化されたデータベースへのルートを作成する  
 次の例では、サービス `//Adventure-Works.com/Expenses` へのルートを作成します。 サービスは、ミラー化されたデータベースでホストされています。 ミラー化されたデータベースのうちの 1 つが置かれているアドレスは `services.Adventure-Works.com:1234`、もう 1 つが置かれているアドレスは `services-mirror.Adventure-Works.com:1234` です。  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. ルーティング用のサービス名を使用するルートを作成する  
 次の例では、メッセージの送信先となるネットワーク アドレスを決定するために、サービス名を使用するルートが作成されます。 ネットワーク アドレスとして `'TRANSPORT'` を指定するルートは、他のルートより照合の優先度が低いことに注意してください。  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>参照  
 [ALTER ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
