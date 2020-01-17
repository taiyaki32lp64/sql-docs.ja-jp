---
title: SQL Server のデータベース ミラーリング
description: データベースミラーリング機能について説明します。
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 89befaff-bb46-4290-8382-e67cdb0e3de9
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 1c78f52f376ff6c333b952b8d013e17eefce45ea
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452272"
---
# <a name="database-mirroring-in-sql-server"></a>SQL Server のデータベース ミラーリング

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server のデータベース ミラーリング機能を使用すると、スタンバイ サーバー上に SQL Server データベースのコピー、つまりミラーを保持できます。 ミラーリングによって、データの2つのコピーが常に存在することが保証されるため、高可用性と完全なデータ冗長性が実現します。 Microsoft SqlClient Provider for SQL Server は、データベース ミラーリングの暗黙的なサポートを提供するので、SQL Server データベース用に構成されていれば、開発者が何らかの処理を行ったり、コードを作成したりする必要はありません。 さらに、<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトは、<xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A> でフェールオーバーパートナーサーバーの名前を指定できる明示的な接続モードをサポートしています。  
  
次の簡略化された一連のイベントは、ミラーリング用に構成されたデータベースを対象とする <xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトに対して発生します。  
  
1. クライアントアプリケーションがプリンシパルデータベースに正常に接続し、サーバーがパートナーサーバーの名前を返します。この名前がクライアントにキャッシュされます。  
  
2. プリンシパルデータベースを含むサーバーで障害が発生した場合、または接続が中断された場合、接続とトランザクションの状態は失われます。 クライアントアプリケーションは、プリンシパルデータベースへの接続を再確立しようとして失敗します。  
  
3. その後、クライアントアプリケーションは、パートナーサーバー上のミラーデータベースへの接続の確立を透過的に試行します。 成功した場合、接続はミラーデータベースにリダイレクトされ、その後、新しいプリンシパルデータベースになります。  
  
## <a name="specifying-the-failover-partner-in-the-connection-string"></a>接続文字列でのフェールオーバーパートナーの指定  
接続文字列にフェールオーバーパートナーサーバーの名前を指定した場合、クライアントアプリケーションが最初に接続したときにプリンシパルデータベースが使用できなくなると、クライアントはフェールオーバーパートナーとの接続を透過的に試行します。  
  
```csharp
";Failover Partner=PartnerServerName"  
```  
  
フェールオーバーパートナーサーバーの名前を省略した場合、クライアントアプリケーションが最初に接続したときにプリンシパルデータベースが使用できなくなると、<xref:Microsoft.Data.SqlClient.SqlException> が発生します。  
  
<xref:Microsoft.Data.SqlClient.SqlConnection> が正常に開かれると、フェールオーバーパートナー名がサーバーから返され、接続文字列で指定された値が置き換えられます。  
  
> [!NOTE]
>  データベースミラーリングシナリオでは、接続文字列で初期カタログまたはデータベース名を明示的に指定する必要があります。 クライアントが、初期カタログやデータベースが明示的に指定されていない接続に関するフェールオーバー情報を受信する場合は、このフェールオーバー情報はキャッシュされず、アプリケーションはプリンシパル サーバーでの障害発生時にフェールオーバーを試行しません。 接続文字列にフェールオーバーパートナーの値が含まれていても、初期カタログまたはデータベースの値がない場合は、`InvalidArgumentException` が発生します。  
  
## <a name="retrieving-the-current-server-name"></a>現在のサーバー名を取得しています  
フェールオーバーが発生した場合は、<xref:Microsoft.Data.SqlClient.SqlConnection> オブジェクトの <xref:Microsoft.Data.SqlClient.SqlConnection.DataSource%2A> プロパティを使用して、現在の接続が実際に接続されているサーバーの名前を取得できます。 次のコード片では、接続変数が開いている <xref:Microsoft.Data.SqlClient.SqlConnection> を参照していると仮定して、アクティブなサーバーの名前を取得します。  
  
フェールオーバーイベントが発生し、接続がミラーサーバーに切り替わると、**データソース**プロパティが更新され、ミラー名が反映されます。  
  
```csharp  
string activeServer = connection.DataSource;  
```  
  
## <a name="sqlclient-mirroring-behavior"></a>SqlClient ミラーリングの動作  
クライアントは、常に現在のプリンシパルサーバーへの接続を試みます。 失敗した場合は、フェールオーバーパートナーを試行します。 ミラーデータベースがパートナーサーバーのプリンシパルロールに既に切り替えられている場合、接続は成功し、新しいプリンシパルミラーマッピングがクライアントに送信され、呼び出し元の <xref:System.AppDomain> の有効期間にわたってキャッシュされます。 このマッピングは永続ストレージには格納されないため、別の **AppDomain** 内またはプロセス内で次回の接続に使用することはできません。 ただし、同一の **AppDomain** 内では次回の接続に使用できます。 同一または別のコンピューター上で実行されている、別の **AppDomain** またはプロセスには常に接続のプールがあり、これらの接続はリセットされません。 このとき、プライマリ データベースがダウンし、各プロセスまたは **AppDomain** が失敗した場合、プールは自動的に消去されます。  
  
> [!NOTE]
>  サーバーでのミラーリングのサポートは、データベースごとに構成されます。 マルチパート名を使用して、または現在のデータベースを変更することによって、プリンシパル/ミラーセットに含まれていない他のデータベースに対してデータ操作操作を実行する場合、これらの他のデータベースに加えられた変更は、エラーが発生しても伝達されません。 ミラー化されていないデータベースでデータが変更されても、エラーは生成されません。 開発者は、このような操作の考えられる影響を評価する必要があります。  
  
## <a name="next-steps"></a>次の手順
### <a name="database-mirroring-resources"></a>データベース ミラーリングのリソース  
ミラーリングの構成、配置、管理の概念に関するドキュメントや情報については、SQL Server ドキュメントの次のリソースを参照してください。  
  
|リソース|[説明]|  
|--------------|-----------------|  
|[データベース ミラーリング](../../../database-engine/database-mirroring/database-mirroring-sql-server.md)|SQL Server でのミラーリングの設定と構成方法について説明します。|  
