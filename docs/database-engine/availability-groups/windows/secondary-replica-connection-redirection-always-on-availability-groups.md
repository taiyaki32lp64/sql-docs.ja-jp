---
title: プライマリ レプリカへの読み取り/書き込み接続のリダイレクト
description: 接続文字列で指定されている対象サーバーに関係なく、読み取り/書き込み接続を Always On 可用性グループのプライマリ レプリカに常にリダイレクトする方法について説明します。
ms.custom: seo-lt-2019
ms.date: 01/09/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: article
helpviewer_keywords:
- connection access to availability replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], readable secondary replicas
- active secondary replicas [SQL Server], read-only access to
- readable secondary replicas
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: ''
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8bf76e0929dea69758b1f9152af0df8f3170227d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75235203"
---
# <a name="secondary-to-primary-replica-readwrite-connection-redirection-always-on-availability-groups"></a>セカンダリ レプリカからプライマリ レプリカへの読み取り/書き込み接続のリダイレクト (Always On 可用性グループ)

[!INCLUDE[appliesto](../../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] CTP 2.0 では、"*Always On 可用性グループに対するセカンダリ レプリカからプライマリ レプリカへの読み取り/書き込み接続のリダイレクト*" が導入されています。 すべてのオペレーティング システム プラットフォームで、読み取り/書き込み接続のリダイレクトを利用できます。 接続文字列に指定されたターゲット サーバーに関係なく、クライアント アプリケーションの接続先をプライマリ レプリカにすることができます。 

たとえば、接続文字列内の接続先がセカンダリ レプリカであるとします。 可用性グループ (AG) の構成と接続文字列の設定によって、接続をプライマリ レプリカに自動的にリダイレクトできます。 

## <a name="use-cases"></a>ユース ケース

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] より前のバージョンでは、プライマリ レプリカへのユーザー トラフィックは、AG リスナーおよび対応するクラスター リソースによってリダイレクトされ、フェールオーバー後に再接続されるようになっています。 [!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] では、この AG リスナー機能は引き続きサポートされますが、リスナーを含めることができないシナリオのためにレプリカの接続のリダイレクトが追加されています。 次に例を示します。

* SQL Server の可用性グループに統合されているクラスター テクノロジでは、リスナーに似た機能が提供されない 
* 構成が複雑になり、エラーが発生しがちであり、複数のコンポーネントが関係するせいでトラブルシューティングが困難な、クラウドや Pacemaker を使用するマルチサブネット フローティング IP のようなマルチサブネット構成である
* 手動でのフェールオーバー時に透過的に再接続するためのわかりやすいメカニズムがないため、読み取りのスケールアウト、またはディザスター リカバリーとクラスターの種類が `NONE` である

## <a name="requirement"></a>要件

セカンダリ レプリカに読み取り/書き込み接続要求をリダイレクトするには:
* セカンダリ レプリカがオンラインである必要があります。 
* レプリカの仕様の `PRIMARY_ROLE` に `READ_WRITE_ROUTING_URL` が含まれている必要があります。
* 接続文字列に `ApplicationIntent` として `ReadWrite` が定義されている必要があります (これは既定値です)。

## <a name="set-read_write_routing_url-option"></a>READ_WRITE_ROUTING_URL オプションを設定する

読み取り/書き込み接続を構成するには、AG を作成するときに、プライマリ レプリカに対して `READ_WRITE_ROUTING_URL` を設定する必要があります。 

[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] では、`<add_replica_option>` 仕様に `READ_WRITE_ROUTING_URL` が追加されています。 次のトピックを参照してください。 

* [CREATE AVAILABILITY GROUP](../../../t-sql/statements/create-availability-group-transact-sql.md)
* [ALTER AVAILABILITY GROUP](../../../t-sql/statements/alter-availability-group-transact-sql.md)


### <a name="primary_roleread_write_routing_url-not-set-default"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL) が設定されていない (既定の設定) 

既定では、レプリカには読み取り/書き込み接続のリダイレクトは設定されていません。 接続要求がセカンダリ レプリカによってどのように処理されるかは、セカンダリ レプリカが接続を許可するように設定されているかどうかと、接続文字列内の `ApplicationIntent` 設定によって決まります。 次の表は、`SECONDARY_ROLE (ALLOW CONNECTIONS = )` と `ApplicationIntent` に基づくセカンダリ レプリカによる接続の処理方法を示しています。

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/> Default|接続失敗|接続失敗|接続成功<br/>読み取り成功<br/>書き込み失敗|
|`ApplicationIntent=ReadOnly`|接続失敗|接続成功|接続成功

上の表に示した既定の動作は、[!INCLUDE[sssqlv15-md](../../../includes/sssqlv15-md.md)] より前のバージョンの SQL Server と同じです。 

### <a name="primary_roleread_write_routing_url-set"></a>PRIMARY_ROLE(READ_WRITE_ROUTING_URL) が設定されている 

読み取り/書き込み接続のリダイレクトを設定すると、レプリカによる接続要求の処理方法が変わります。 接続動作は、引き続き `SECONDARY_ROLE (ALLOW CONNECTIONS = )` と `ApplicationIntent` の設定によって決まります。 次の表は、`READ_WRITE_ROUTING` が設定されたセカンダリ レプリカによる `SECONDARY_ROLE (ALLOW CONNECTIONS = )` と `ApplicationIntent` に基づく接続の処理方法を示しています。

||`SECONDARY_ROLE (ALLOW CONNECTIONS = NO)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = READ_ONLY)`|`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)`|
|-----|-----|-----|-----|
|`ApplicationIntent=ReadWrite`<br/>Default|接続失敗|接続失敗|プライマリへの接続のルーティング|
|`ApplicationIntent=ReadOnly`|接続失敗|接続成功|接続成功

上の表は、プライマリ レプリカに `READ_WRITE_ROUTING_URL` が設定されているときに、`SECONDARY_ROLE (ALLOW CONNECTIONS = ALL)` であり、接続に `ReadWrite` が指定されている場合に、セカンダリ レプリカによって接続がプライマリ レプリカにリダイレクトされることを示しています。

## <a name="example"></a>例 

この例では、可用性グループには 3 つのレプリカがあります。
* COMPUTER01 上のプライマリ レプリカ
* COMPUTER02 上の同期セカンダリ レプリカ
* COMPUTER03 上の非同期セカンダリ レプリカ

次の図は、可用性グループを表しています。

![元の可用性グループ](media/replica-connection-redirection-always-on-availability-groups/01_originalAG.png)

この AG は、次の Transact-SQL スクリプトによって作成されています。 この例では、各レプリカに `READ_WRITE_ROUTING_URL` が指定されています。
```sql
CREATE AVAILABILITY GROUP MyAg   
     WITH ( CLUSTER_TYPE =  NONE )  
   FOR   
     DATABASE  <Database1>   
   REPLICA ON   
      'COMPUTER01' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER01.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' ),
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER02, COMPUTER03),
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER01.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER02' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER02.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL, 
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER03),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER02.<domain>.<tld>:1433' )   
         SESSION_TIMEOUT = 10  
         ),   
      'COMPUTER03' WITH   
         (  
         ENDPOINT_URL = 'TCP://COMPUTER03.<domain>.<tld>:5022',  
         AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,  
         FAILOVER_MODE = MANUAL,  
         SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL,   
            READ_ONLY_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' ),  
         PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE,   
            READ_ONLY_ROUTING_LIST = (COMPUTER01, COMPUTER02),  
            READ_WRITE_ROUTING_URL = 'TCP://COMPUTER03.<domain>.<tld>:1433' )  
         SESSION_TIMEOUT = 10  
         );
GO  
```
   - `<domain>.<tld>`
      - 完全修飾ドメイン名のドメインと最上位ドメイン。 たとえば、「 `corporation.com` 」のように入力します。


### <a name="connection-behaviors"></a>接続動作

次の図では、クライアント アプリケーションが `ApplicationIntent=ReadWrite` で COMPUTER02 に接続します。 この接続は、プライマリ レプリカにリダイレクトされます。 

![元の可用性グループ](media/replica-connection-redirection-always-on-availability-groups/02_redirectionAG.png)

セカンダリ レプリカでは、読み取り/書き込み呼び出しがプライマリ レプリカにリダイレクトされます。 どちらのレプリカへの読み取り/書き込み接続も、プライマリ レプリカにリダイレクトされます。 

次の図では、プライマリ レプリカが手動で COMPUTER02 にフェールオーバーされています。 クライアント アプリケーションは、`ApplicationIntent=ReadWrite` で COMPUTER01 に接続します。 この接続は、プライマリ レプリカにリダイレクトされます。 

![元の可用性グループ](media/replica-connection-redirection-always-on-availability-groups/03_redirectionAG.png)


## <a name="sql-server-instance-offline"></a>SQL Server インスタンスのオフライン状態

接続文字列に指定された SQL Server インスタンスを利用できない場合 (インスタンスが停止している) 場合、ターゲット サーバー上のレプリカに割り当てられているロールに関係なく、接続は失敗します。 長時間にわたるアプリケーションのダウンタイムを避けるには、接続文字列内に代替の `FailoverPartner` を構成します。 アプリケーションでは、フェールオーバーの実行中はオフライン状態になるプライマリ レプリカとセカンダリ レプリカに対応するための再試行ロジックを実装する必要があります。 接続文字列については、「[SqlConnection.ConnectionString プロパティ](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.connectionstring.aspx)」を参照してください。

## <a name="see-also"></a>参照

[Always On 可用性グループの概要 &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 
[可用性レプリカに対するクライアント接続アクセスについて &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   

[可用性グループ リスナー、クライアント接続、およびアプリケーションのフェールオーバー &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md) 
