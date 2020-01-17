---
title: ALTER ROUTE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2018
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 1e05ad220147e7f46bfaa66127fcc492aaeae6a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927184"
---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既存のルートに関するルート情報を変更します。 

  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>引数  
 *route_name*  
 変更するルートの名前を指定します。 サーバー名、データベース名、スキーマ名は指定できません。  
  
 WITH  
 変更するルート情報を定義するための句を、WITH の後に指定します。  
  
 SERVICE_NAME **='** _service\_name_ **'**  
 このルートが示すリモート サービスの名前を指定します。 *service_name* はリモート サービスで使用される名前と正確に一致する必要があります。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] は *service_name* をバイト単位で照合します。 つまり、この比較では大文字と小文字が区別され、現在の照合順序は考慮されません。 **'SQL/ServiceBroker/BrokerConfiguration'** というサービス名を持つルートは、Broker Configuration Notice サービスへのルートです。 このサービスへのルートは、ブローカー インスタンスを指定できない場合があります。  
  
 SERVICE_NAME 句を省略した場合、ルートのサービス名は変更されません。  
  
 BROKER_INSTANCE **='** _broker\_instance_ **'**  
 発信先サービスをホストするデータベースを指定します。 *broker_instance* パラメーターは、リモート データベース用のブローカー インスタンス識別子である必要があります。これは選択したデータベースで次のクエリを実行することにより取得できます。  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 BROKER_INSTANCE 句を省略した場合、ルートのブローカー インスタンスは変更されません。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 LIFETIME **=** _route\_lifetime_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がルーティング テーブルにルートを保持する時間を秒単位で指定します。 有効期間が終了するとルートは期限切れとなり、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、新しいメッセージ交換用のルートを選択するときに、そのルートは考慮されなくなります。 この句を省略した場合、ルートの有効期限は変更されません。  
  
 ADDRESS **='** _next\_hop\_address_'  

 Azure SQL Database マネージド インスタンスの場合、`ADDRESS` はローカルである必要があります。

 このルート用のネットワーク アドレスを指定します。 *next_hop_address* の次の形式で TCP/IP アドレスを指定します。  
  
 **TCP://** { *dns_name* | *netbios_name* |*ip_address* } **:** *port_number*  
  
 指定した *port_number* は、指定したコンピューターにおける [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの [!INCLUDE[ssSB](../../includes/sssb-md.md)] エンドポイント用のポート番号と一致する必要があります。 これは選択したデータベースで次のクエリを実行することにより取得できます。  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 ルートの *next_hop_address* が **'LOCAL'** になっている場合、メッセージは現在の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス内のサービスに配信されます。  
  
 ルートの *next_hop_address* が **'TRANSPORT'** になっている場合、ネットワーク アドレスは、サービス名の中にあるネットワーク アドレスに基づいて決まります。 **'TRANSPORT'** を指定するルートは、サービス名またはブローカー インスタンスを指定できます。  
  
 *next_hop_address* にデータベース ミラーのプリンシパル サーバーを指定した場合は、ミラー サーバーの MIRROR_ADDRESS も指定する必要があります。 それ以外の場合、このルートではミラー サーバーへの自動フェールオーバーは行われません。  
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
 MIRROR_ADDRESS **='** _next\_hop\_mirror\_address_ **'**  
 プリンシパル サーバーが *next_hop_address* となっているミラーリング ペアのミラー サーバーのネットワーク アドレスを指定します。 *next_hop_mirror_address* は、次の形式で TCP/IP アドレスを指定します。  
  
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
  
> [!NOTE]  
>  このオプションは、包含データベースでは使用できません。  
  
## <a name="remarks"></a>Remarks  
 ルートを格納するルーティング テーブルは、**sys.routes** カタログ ビューを使用して読み取ることができるメタデータ テーブルです。 このルーティング テーブルは、CREATE ROUTE、ALTER ROUTE、DROP ROUTE ステートメントでのみ更新できます。  
  
 ALTER ROUTE コマンドで指定されない句は、変更されません。 したがって、ALTER を使用して、ルートのタイムアウトを無効にしたり、ルートをすべてのサービス名やブローカー インスタンスと照合したりするようにルートを変更することはできません。 このようなルートの特性を変更するには、既存のルートを削除して新しいルートを作成し、新しい情報を指定する必要があります。  
  
 ルートが *next_hop_address* に **'TRANSPORT'** を指定した場合、ネットワーク アドレスはサービスの名前に基づいて決定されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、*next_hop_address* のネットワーク アドレスが有効な形式であれば、このネットワーク アドレスで始まるサービス名が適切に処理されます。 名前に有効なネットワーク アドレスが含まれているサービスは、そのサービス名のネットワーク アドレスにルートされます。  
  
 ルートで指定されているサービス、ネットワーク アドレス、ブローカー インスタンス識別子のいずれか、またはすべてが同じであれば、ルーティング テーブルにはルートをいくつでも含めることができます。 このような場合、[!INCLUDE[ssSB](../../includes/sssb-md.md)] でルートを選択するときには、メッセージ交換で指定された情報とルーティング テーブル内の情報を照合して、最も正確に一致する情報を取得するためのプロシージャが使用されます。  
  
 サービスの AUTHORIZATION を変更するには、ALTER AUTHORIZATION ステートメントを使用します。  
  
## <a name="permissions"></a>アクセス許可  
 ルートを変更する権限は、既定ではルートの所有者、**db_ddladmin** 固定データベース ロールまたは **db_owner** 固定データベース ロールのメンバー、**sysadmin** 固定サーバー ロールのメンバーに与えられています。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-changing-the-service-for-a-route"></a>A. ルートのサービスを変更する  
 次の例では、`ExpenseRoute` ルートが示すサービスを、リモート サービス `//Adventure-Works.com/Expenses` に変更します。  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>B. ルートのターゲット データベースを変更する  
 次の例では、`ExpenseRoute` ルートの対象データベースを、一意識別子 `D8D4D268-00A3-4C62-8F91-634B89B1E317.` によって指定されるデータベースに変更します。  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>C. ルートのアドレスを変更する  
 次の例では、IP アドレスが `10.2.19.72` のホストで、`ExpenseRoute` ルートのネットワーク アドレスが TCP ポート `1234` に変更されます。  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>D. ルートのデータベースとアドレスを変更する  
 次の例では、`ExpenseRoute` ルートのネットワーク アドレスを、DNS 名 `1234` のホスト、TCP ポート `www.Adventure-Works.com` に変更します。 また、対象データベースを、一意識別子 `D8D4D268-00A3-4C62-8F91-634B89B1E317` によって指定されるデータベースに変更します。  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>参照  
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [DROP ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
