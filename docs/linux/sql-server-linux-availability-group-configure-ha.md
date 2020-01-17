---
title: SQL Server on Linux の可用性グループを構成する
description: Linux で高可用性を実現するために SQL Server の Always On 可用性グループ (AG) を作成する方法について説明します。
author: MikeRayMSFT
ms.custom: seo-lt-2019
ms.author: mikeray
ms.reviewer: vanto
ms.date: 08/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 2e234e0057db852b6b741a0103412bbacd108287
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558399"
---
# <a name="configure-sql-server-always-on-availability-group-for-high-availability-on-linux"></a>Linux で高可用性を実現するために SQL Server の Always On 可用性グループを構成する

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

この記事では、Linux 上で、高可用性を実現するために SQL Server の Always On 可用性グループ (AG) を作成する方法について説明します。 AG には 2 種類の構成が存在します。 "*高可用性*" の構成では、クラスター マネージャーを使ってビジネス継続性を提供します。 この構成には、読み取りスケールのレプリカを含めることもできます。 このドキュメントでは、高可用性のための AG を作成する方法について説明します。

"*読み取りスケール*" のために、クラスター マネージャーなしで AG を作成することもできます。 読み取りスケールの AG では、パフォーマンス スケールアウトのための読み取り専用レプリカだけが提供されます。高可用性は提供されません。 読み取りスケールの AG を作成するには、「[Linux で読み取りスケールの SQL Server 可用性グループを構成する](sql-server-linux-availability-group-configure-rs.md)」をご覧ください。

高可用性とデータ保護が保証される構成のためには、2 つまたは 3 つの同期コミット レプリカが必要です。 3 つの同期レプリカを使う場合は、1 台のサーバーが使用できない場合でも AG が自動的に復旧されます。 詳細については、「[可用性グループ構成の高可用性とデータ保護](sql-server-linux-availability-group-ha.md)」をご覧ください。 

すべてのサーバーは物理または仮想である必要があり、仮想サーバーは同じ仮想化プラットフォーム上にある必要があります。 この要件が生じるのは、フェンス エージェントがプラットフォーム固有であるためです。 [ゲスト クラスターのポリシー](https://access.redhat.com/articles/29440#guest_policies)に関するページをご覧ください。

## <a name="roadmap"></a>ロードマップ

高可用性のために Linux サーバー上に AG を作成する手順は、Windows Server フェールオーバー クラスターでの手順とは異なります。 以下に、おおまかな手順を説明します。 

1. [3 台のクラスター サーバーで SQL Server を構成します](sql-server-linux-setup.md)。

   >[!IMPORTANT]
   >AG 内の 3 台のサーバーはすべて同じプラットフォーム (物理または仮想) 上に配置する必要があります。これは、Linux の高可用性ではサーバー上のリソースを分離するためにフェンス エージェントが使われるためです。 フェンス エージェントは、各プラットフォームに固有のものです。

2. AG を作成します。 この手順について、この現在の記事で説明します。 

3. Pacemaker などのクラスター リソース マネージャーを構成します。
   
   クラスター リソース マネージャーを構成する方法は、特定の Linux ディストリビューションによって異なります。 ディストリビューション固有の手順については、以下のリンクをご覧ください。 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md)
   * [SUSE](sql-server-linux-availability-group-cluster-sles.md)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md)

   >[!IMPORTANT]
   >運用環境では、高可用性のために STONITH のようなフェンス エージェントが必要です。 このドキュメントに含まれているデモでは、フェンス エージェントは使用しません。 このデモはテストと検証専用です。 
   
   >Linux クラスターでは、フェンスを使用して、クラスターが既知の状態に戻されます。 フェンスを構成する方法は、ディストリビューションと環境によって異なります。 現時点では、一部のクラウド環境ではフェンスを利用できません。 詳細については、[RHEL 高可用性クラスターのサポート ポリシー (仮想化プラットフォーム)](https://access.redhat.com/articles/29440) に関するページをご覧ください。
   
   >SLES については、[SUSE Linux Enterprise High Availability Extension](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#cha.ha.fencing) に関するページをご覧ください。

5. AG をリソースとしてクラスターに追加します。  

   AG をリソースとしてクラスターに追加する方法は、Linux ディストリビューションによって異なります。 ディストリビューション固有の手順については、以下のリンクをご覧ください。 

   * [RHEL](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource)
   * [SLES](sql-server-linux-availability-group-cluster-sles.md#configure-the-cluster-resources-for-sql-server)
   * [Ubuntu](sql-server-linux-availability-group-cluster-ubuntu.md#create-availability-group-resource)

[!INCLUDE [Create Prerequisites](../includes/ss-linux-cluster-availability-group-create-prereq.md)]

## <a name="create-the-ag"></a>AG を作成する

このセクションの例では、Transact-SQL を使って可用性グループを作成する方法について説明します。 SQL Server Management Studio の可用性グループ ウィザードを使うこともできます。 ウィザードを使って AG を作成した場合、AG にレプリカを参加させるとエラーが返されます。 これを修正するには、すべてのレプリカの AG のペースメーカーに `ALTER`、`CONTROL`、および `VIEW DEFINITIONS` を付与します。 プライマリ レプリカにアクセス許可を付与したら、ウィザードを使って AG にノードを参加させます。ただし、HA を正常に機能させるために、すべてのレプリカに対して権限を付与します。

自動フェールオーバーを確実に行う高可用性を構成する場合、AG には少なくとも 3 つのレプリカが必要です。 次のいずれかの構成で高可用性をサポートできます。

- [3 つの同期レプリカ](sql-server-linux-availability-group-ha.md#threeSynch)

- [2 つの同期レプリカと 1 つの構成レプリカ](sql-server-linux-availability-group-ha.md#twoSynch)

詳しくは、「[可用性グループ構成の高可用性とデータ保護](sql-server-linux-availability-group-ha.md)」をご覧ください。

>[!NOTE]
>可用性グループには、追加の同期または非同期レプリカを含めることができます。 

Linux で高可用性のための AG を作成します。 `CLUSTER_TYPE = EXTERNAL` を指定した [CREATE AVAILABILITY GROUP](https://docs.microsoft.com/sql/t-sql/statements/create-availability-group-transact-sql) を使います。 

* 可用性グループ - `CLUSTER_TYPE = EXTERNAL`: 外部クラスター エンティティにより AG が管理されることを指定します。 Pacemaker は外部クラスター エンティティの例です。 AG のクラスターの種類が外部である場合は、 

* プライマリおよびセカンダリ レプリカを `FAILOVER_MODE = EXTERNAL` に設定します。 
   レプリカが外部クラスター マネージャー (Pacemaker など) と連携することを指定します。 

以下の Transact-SQL スクリプトでは、`ag1` という名前の高可用性の AG が作成されます。 このスクリプトでは、`SEEDING_MODE = AUTOMATIC` で AG レプリカが構成されます。 この設定により、各セカンダリ サーバー上に SQL Server によってデータベースが自動作成されます。 ご利用の環境に合わせて次のスクリプトを変更してください。 `<node1>`、`<node2>`、または `<node3>` の値を、レプリカをホストする SQL Server インスタンスの名前に置き換えます。 `<5022>` を、データ ミラーリング エンドポイント用に設定したポートに置き換えます。 AG を作成するには、プライマリ レプリカをホストしている SQL Server インスタンス上で次の Transact-SQL を実行します。

次のスクリプトの**いずれか 1 つのみ**を実行します。 

- [3 つの同期レプリカを使って可用性グループを作成する](#threeSynch)。
- [2 つの同期レプリカと 1 つの構成レプリカを使って可用性グループを作成する](#configOnly)
- [2 つの同期レプリカを使って可用性グループを作成する](#readScale)。

<a name="threeSynch"></a>

- 3 つの同期レプリカを使って AG を作成する

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
       WITH (DB_FAILOVER = ON, CLUSTER_TYPE = EXTERNAL)
       FOR REPLICA ON
           N'<node1>' 
            WITH (
               ENDPOINT_URL = N'tcp://<node1>:<5022>',
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node2>' 
            WITH ( 
               ENDPOINT_URL = N'tcp://<node2>:<5022>', 
               AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
               FAILOVER_MODE = EXTERNAL,
               SEEDING_MODE = AUTOMATIC
               ),
           N'<node3>'
           WITH( 
              ENDPOINT_URL = N'tcp://<node3>:<5022>', 
              AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
              FAILOVER_MODE = EXTERNAL,
              SEEDING_MODE = AUTOMATIC
              );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```

   >[!IMPORTANT]
   >上記のスクリプトを実行して 3 つの同期レプリカを持つ AG を作成した後は、以下のスクリプトは実行しないでください。

<a name="configOnly"></a>
- 2 つの同期レプリカと 1 つの構成レプリカを使って AG を作成する:

   >[!IMPORTANT]
   >このアーキテクチャでは、任意のエディションの SQL Server を使って 3 番目のレプリカをホストすることができます。 たとえば、SQL Server Express Edition 上で 3 番目のレプリカをホストできます。 Express Edition の場合、有効なエンドポイントの種類は `WITNESS` のみです。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1] 
      WITH (CLUSTER_TYPE = EXTERNAL) 
      FOR REPLICA ON 
       N'<node1>' WITH ( 
          ENDPOINT_URL = N'tcp://<node1>:<5022>', 
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node2>' WITH (  
          ENDPOINT_URL = N'tcp://<node2>:<5022>',  
          AVAILABILITY_MODE = SYNCHRONOUS_COMMIT, 
          FAILOVER_MODE = EXTERNAL, 
          SEEDING_MODE = AUTOMATIC 
          ), 
       N'<node3>' WITH ( 
          ENDPOINT_URL = N'tcp://<node3>:<5022>', 
          AVAILABILITY_MODE = CONFIGURATION_ONLY  
          );
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```
<a name="readScale"></a>

- 2 つの同期レプリカを使って AG を作成する

   同期可用性モードの 2 つのレプリカを含めます。 たとえば、次のスクリプトでは、`ag1` という名前の AG が作成されます。 `node1` および `node2` では、自動シード処理と自動フェールオーバーを備えた、同期モードのレプリカがホストされます。

   >[!IMPORTANT]
   >2 つの同期レプリカを含む AG を作成する場合は、次のスクリプトだけを実行してください。 上記のスクリプトのいずれかを実行している場合は、以下のスクリプトを実行しないでください。 

   ```SQL
   CREATE AVAILABILITY GROUP [ag1]
      WITH (CLUSTER_TYPE = EXTERNAL)
      FOR REPLICA ON
      N'node1' WITH (
         ENDPOINT_URL = N'tcp://node1:5022',
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      ),
      N'node2' WITH ( 
         ENDPOINT_URL = N'tcp://node2:5022', 
         AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
         FAILOVER_MODE = EXTERNAL,
         SEEDING_MODE = AUTOMATIC
      );
        
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
   ```


SQL Server Management Studio または PowerShell を使って、`CLUSTER_TYPE=EXTERNAL` で AG を構成することもできます。 

### <a name="join-secondary-replicas-to-the-ag"></a>セカンダリ レプリカを AG に参加させる

ペースメーカーのユーザーは、すべてのレプリカ上の可用性グループに対して `ALTER`、`CONTROL`、`VIEW DEFINITION` のアクセス許可を持っている必要があります。 アクセス許可を付与するには、プライマ リレプリカと各セカンダリ レプリカ上に可用性グループが作成された後、それらが可用性グループに追加された直後に、次の Transact-SQL スクリプトを実行します。 このスクリプトを実行する前に、`<pacemakerLogin>` をペースメーカーのユーザー アカウントに置き換えます。 ペースメーカーのログインがない場合、[ペースメーカーの SQL サーバー ログインを作成してください](sql-server-linux-availability-group-cluster-ubuntu.md#create-a-sql-server-login-for-pacemaker)。

```sql
GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::ag1 TO <pacemakerLogin>
GRANT VIEW SERVER STATE TO <pacemakerLogin>
```

次の Transact-SQL スクリプトを実行すると、`ag1` という名前の AG に SQL Server インスタンスを参加させることができます。 ご利用の環境に合わせてスクリプトを変更してください。 セカンダリ レプリカをホストしている各 SQL Server インスタンス上で、次の Transact-SQL を実行して AG に参加させます。

```sql
ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
         
ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE;
```

[!INCLUDE [Create Post](../includes/ss-linux-cluster-availability-group-create-post.md)]

>[!IMPORTANT]
>AG を作成したら、高可用性のために Pacemaker のようなクラスター テクノロジとの統合を構成する必要があります。 AG を使った読み取りスケール構成の場合 ([!INCLUDE [SQL Server version](../includes/sssqlv14-md.md)] 以降)、クラスターの設定は必要ありません。

このドキュメントに記載されている手順に従った場合は、まだクラスター化されていない AG ができます。 次の手順は、クラスターを追加することです。 この構成は、読み取りスケール/負荷分散のシナリオに対しては有効ですが、高可用性の場合は完全ではありません。 高可用性を実現するには、AG をクラスター リソースとして追加する必要があります。 手順については、「[次の手順](#next-steps)」をご覧ください。 

## <a name="notes"></a>メモ

>[!IMPORTANT]
>クラスターを構成し、AG をクラスター リソースとして追加した後は、Transact-SQL を使って AG リソースをフェールオーバーすることはできません。 Linux 上の SQL Server クラスター リソースは、Windows Server フェールオーバー クラスター (WSFC) ほど、オペレーティング システムと緊密に結合されていません。 SQL Server サービスでは、クラスターの存在は認識されません。 すべてのオーケストレーションは、クラスター管理ツールを使用して実行されます。 RHEL または Ubuntu では、`pcs` を使います。 SLES では `crm` を使います。 

>[!IMPORTANT]
>AG がクラスター リソースの場合、現在のリリースには、非同期レプリカへのデータ損失を伴う強制フェールオーバーが機能しないという既知の問題があります。 これは今後のリリースで修正される予定です。 同期レプリカへの手動または自動フェールオーバーは成功します。


## <a name="next-steps"></a>次のステップ

[SQL Server 可用性グループ クラスター リソースに対して Red Hat Enterprise Linux クラスターを構成する](sql-server-linux-availability-group-cluster-rhel.md)

[SQL Server 可用性グループ クラスター リソースに対して SUSE Linux Enterprise Server クラスターを構成する](sql-server-linux-availability-group-cluster-sles.md)

[SQL Server 可用性グループ クラスター リソースに対して Ubuntu クラスターを構成する](sql-server-linux-availability-group-cluster-ubuntu.md)
