---
title: ドメインに依存しない可用性グループを作成する
description: ワークグループ クラスターを使用する可用性グループを作成する手順について説明します。 これにより SQL Server 2016 (以降) で Active Directory Domain Services を必要としない、従って各サーバーが同じドメインの一部となる必要がない Always On 可用性グループを WSFC 上に展開できるようになります。
ms.custom: seodec18
ms.date: 09/25/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], domain independent
ms.assetid: ''
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: b57d3443ab83ead35d92615ad6c718cde6977097
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68000225"
---
# <a name="create-a-domain-independent-availability-group"></a>ドメインに依存しない可用性グループを作成する
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Always On 可用性グループ (AG) には、基になる Windows Server フェールオーバー クラスター (WSFC) が必要です。 Windows Server 2012 R2 を使用して WSFC を展開するには、WSFC (ノードとも呼ばれる) に参加しているサーバーが同じドメインに追加されていることが常に必要です。 Active Directory Domain Services (AD DS) の詳細については、[ここ](https://technet.microsoft.com/library/cc759073(v=ws.10).aspx)を参照してください。

データベース ミラーリング (DBM) は、このような依存関係を持たずに、証明書を使用して複数のデータ センターに展開できるため、AD DS と WSFC の依存関係は、DBM の構成で以前に展開されたものよりも複雑です。  複数のデータ センターに広がる従来の可用性グループでは、すべてのサーバーが同じ Active Directory ドメインに参加している必要があります。異なるドメインでは、信頼されたドメインであっても動作しません。 すべてのサーバーが、同じ WSFC のノードである必要があります。 この構成を次の図に示します。 SQL Server 2016 には、異なる方法でこの目的を達成することもできる、分散された可用性グループもあります。


![同じドメインに接続された 2 つのデータ センターに広がる WSFC][1]

Windows Server 2012 R2 では、可用性グループで使用できる Windows Server フェールオーバー クラスターの特殊な形式である、[Active Directory がデタッチされたクラスター](https://technet.microsoft.com/library/dn265970.aspx)を導入しました。 この種類の WSFC は、同じ Active Directory ドメインにドメイン参加しているノードがまだ必要です。ただし、この場合、WSFC は DNS を使用していますが、ドメインは使用しません。 ドメインが引き続き含まれているため、Active Directory がデタッチされたクラスターでは、完全にドメインを必要としないエクスペリエンスを提供することはまだありません。

Windows Server 2016 では、Active Directory がデタッチされたクラスター (ワークグループ クラスター) を基にした新しい種類の Windows Server フェールオーバー クラスターを導入しました。 ワークグループ クラスターによって、SQL Server 2016 は、AD DS を必要としない WSFC の上部に可用性グループを展開することができます。 SQL Server では、データベース ミラーリングのシナリオで証明書が必要なように、エンドポイントのセキュリティに証明書を使用する必要があります。  可用性グループのこの種類は、ドメインに依存しない可用性グループと呼ばれます。 基になるワークグループ クラスターでの可用性グループの展開では、WSFC を構成するノードに対して次の組み合わせをサポートします。
- ドメインに参加しているノードはありません。
- すべてのノードが異なるドメインに参加しています。
- ノードがドメインに参加しているノートとドメインに参加していないノードを組み合わせて混在しています。

次の図は、Data Center 1 のノードはドメインに参加していますが、Data Center 2 のノードは DNS のみを使用する場合のドメインに依存しない可用性グループの例を示します。 この場合、WSFC のノードになるすべてのサーバーで DNS サフィックスを設定します。 可用性グループにアクセスしているすべてのアプリケーションとサーバーが、同じ DNS 情報を参照する必要があります。


![1 つのドメインに参加している 2 つのノードを含むワークグループ クラスター][2]

ドメインに依存しない可用性グループは、マルチサイトまたはディザスター リカバリー シナリオに使用するためだけではありません。 これは、1 つのデータ センターに展開することができ、[基本的な可用性グループ](basic-availability-groups-always-on-availability-groups.md) (Standard Edition 可用性グループとしても知られる) でも使用され、次のように証明書を含むデータベース モニタリングを使用して達成するために使用されるものに同様のアーキテクチャを提供します。


![Standard Edition の AG の高レベルのビュー][3]

ドメインに依存しない可用性グループの展開には、既知の注意事項がいくつかあります。
- クォーラムと共に使用できる監視の種類は、ディスクと[クラウド](https://technet.microsoft.com/windows-server-docs/failover-clustering/deploy-cloud-witness)のみです。クラウドは、Windows Server 2016 の新機能です。 可用性グループによる共有ディスクの使用はほとんどないため、ディスクでは問題があります。
- WSFC の基になるワークグループ クラスター バリアントは、PowerShell を使用してのみ作成できますが、フェールオーバー クラスター マネージャーを使用して管理することができます。
- Kerberos が必要な場合、Active Directory にアタッチされる標準の WSFC を展開する必要があります。ドメインに依存しない可用性グループは、オプションではない可能性があります。
- リスナーが構成されるときは、使用できる DNS に登録される必要があります。 前述のとおり、リスナーに対する Kerberos サポートはありません。
- ドメインが存在しなかったり、連携するように構成されていない可能性があったりするため、SQL Server に接続しているアプリケーションでは、主に SQL Server 認証を使用します。 
- 証明書は、可用性グループの構成で使用されます。

## <a name="set-and-verify-the-dns-suffix-on-all-replica-servers"></a>すべてのレプリカ サーバーで DNS サフィックスを設定および確認する

共通の DNS サフィックスは、ドメインに依存しない可用性グループのワークグループ クラスターに必要です。 可用性グループのレプリカをホストする各 Windows Server に DNS サフィックスを設定および確認するには、次の手順に従います。

1. Windows キー + X キーのショートカットを使用して、[システム] を選択します。
2. コンピューター名と完全なコンピューター名が同じ場合は、DNS サフィックスは設定されていません。 たとえば、コンピューター名が ALLAN の場合、完全なコンピューター名の値は、ALLAN だけにはなりません。 ALLAN.SQLHA.LAB のようになります。 SQLHA.LAB は、DNS サフィックスです。 ワークグループの値は、WORKGROUP となります。 DNS サフィックスを設定する必要がある場合は、[設定の変更] を選択します。
3. [システムのプロパティ] の [コンピューター名] タブで、[変更] をクリックします。
4. [コンピューター名/ドメイン名の変更] ダイアログで、[詳細] をクリックします。
5. [DNS サフィックスと NetBIOS コンピューター名] ダイアログで、プライマリ DNS サフィックスとして、共通の DNS サフィックスを入力します。 
6. [OK] をクリックして、[DNS サフィックスと NetBIOS コンピューター名] ダイアログを閉じます。
7. [OK] をクリックして、[コンピューター名/ドメイン名の変更] ダイアログを閉じます。
8. 変更を有効にするために、サーバーを再起動するようメッセージが表示されます。 [OK] をクリックして、[コンピューター名/ドメイン名の変更] ダイアログを閉じます。
9. [閉じる] をクリックして、[システムのプロパティ] ダイアログを閉じます。
10. 再起動を求めるメッセージが表示されます。 すぐに再起動しない場合は、[後で再起動] をクリックします。それ以外の場合は、[今すぐ再起動する] をクリックします。
11. サーバーが再起動されたら、もう一度システムを確認して、共通の DNS サフィックスが構成されていることを確認します。

![DNS サフィックスの正常に終了した構成][4]

  > [!NOTE]
  > 複数のサブネットを使用していて、静的 DNS がある場合は、フェールオーバーを実行する前にリスナーに関連付けられている DNS レコードを更新するためのプロセスを、用意する必要があります。そうしないと、ネットワーク名がオンラインになりません。

## <a name="create-a-domain-independent-availability-group"></a>ドメインに依存しない可用性グループを作成する

現在、ドメインの独立した可用性グループの作成は、SQL Server Management Studio を使用して完全に達成することはできません。 ドメインに依存しない可用性グループの作成は、標準の可用性グループの作成と基本的に同じですが、特定のアスペクト (証明書の作成など) は Transact-SQL でのみ可能です。 次の例は、2 つのレプリカを持つ可用性グループの構成を想定しています。プライマリが 1 つとセカンダリが 1 つです。 

1. [このリンクの手順を使用して](https://techcommunity.microsoft.com/t5/Failover-Clustering/Workgroup-and-Multi-domain-clusters-in-Windows-Server-2016/ba-p/372059)、すべてが可用性グループに参加するサーバーで構成されるワークグループ クラスターを展開します。 ワークグループ クラスターを構成する前に、共通の DNS サフィックスが既に構成されていることを確認します。
2. 可用性グループに追加する各インスタンスの [Always On 可用性グループ機能を有効にします](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server)。 これには、各 SQL Server インスタンスの再起動が必要がです。
3. プライマリ レプリカをホストするインスタンスごとに、データベース マスター キーが必要です。 マスター キーがまだ存在していない場合は、次のコマンドを実行します。

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'Strong Password';
   GO
   ```

4. プライマリ レプリカとなるインスタンスで、セカンダリ レプリカの着信接続用と、プライマリ レプリカのエンドポイントをセキュリティで保護するために使用される証明書を作成します。

   ```sql
   CREATE CERTIFICATE InstanceA_Cert 
   WITH SUBJECT = 'InstanceA Certificate';
   GO
   ``` 

5. 証明書をバックアップします。 また、必要であれば、秘密キーを使ってさらにセキュリティで保護することもできます。 この例では、秘密キーを使用しません。

   ```sql
   BACKUP CERTIFICATE InstanceA_Cert 
   TO FILE = 'Backup_path\InstanceA_Cert.cer';
   GO
   ```

6. 手順 4 と 5 を繰り返して、InstanceB_Cert などの証明書の適切な名前を使用し、セカンダリ レプリカごとに証明書を作成してバックアップします。
7. プライマリ レプリカでは、可用性グループのセカンダリ レプリカごとにログインを作成する必要があります。 このログインには、ドメインに依存しない可用性グループによって使用されるエンドポイントに接続するアクセス許可が付与されます。 たとえば、InstanceB という名前のレプリカの場合

   ```sql
   CREATE LOGIN InstanceB_Login WITH PASSWORD = 'Strong Password';
   GO
   ```

8. 各セカンダリ レプリカで、プライマリ レプリカのログインを作成します。 このログインには、エンドポイントに接続するアクセス許可が付与されます。 たとえば、InstanceB という名前のレプリカで次を実行します。

   ```sql
   CREATE LOGIN InstanceA_Login WITH PASSWORD = 'Strong Password';
   GO
   ```

9. すべてのインスタンスで、作成されたログインごとにユーザーを作成します。 これは、証明書を復元するときに使用されます。 たとえば、プライマリ レプリカのユーザーを作成するには、次を実行します。

   ```sql
   CREATE USER InstanceA_User FOR LOGIN InstanceA_Login;
   GO
   ```

10. プライマリになる可能性があるレプリカでは、関連するすべてのセカンダリ レプリカでログインとユーザーを作成します。
11. 各インスタンスで、作成されたログインとユーザーがある他のインスタンスに証明書を復元します。 プライマリ レプリカで、すべてのセカンダリ レプリカの証明書を復元します。 各セカンダリで、プライマリ レプリカの証明書を復元します。また、プライマリになる可能性があるその他のレプリカにも復元します。 例:

   ```sql
   CREATE CERTIFICATE [InstanceB_Cert]
   AUTHORIZATION InstanceB_User
   FROM FILE = 'Restore_path\InstanceB_Cert.cer'
   ```

12. レプリカになる各インスタンスに、可用性グループによって使用されるエンドポイントを作成します。 可用性グループの場合は、エンドポイントに DATABASE_MIRRORING の型がある必要があります。 エンドポイントでは、手順 4 で認証のインスタンスのために作成した証明書を使用します。 以下の構文は、証明書を使用してエンドポイントを作成する例を示しています。 適切な暗号化方法と、環境に関連するその他のオプションを使用します。 使用できるオプションの詳細については、「[CREATE ENDPOINT (Transact-SQL)](../../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。

   ```sql
   CREATE ENDPOINT DIAG_EP
   STATE = STARTED
   AS TCP (   
    LISTENER_PORT = 5022,
    LISTENER_IP = ALL
         )
   FOR DATABASE_MIRRORING (
    AUTHENTICATION = CERTIFICATE InstanceX_Cert,
    ROLE = ALL
         )
   ```

13. エンドポイントに接続できるように、手順 9 のインスタンスで作成された各ユーザーに権限を割り当てます。 

   ```sql
   GRANT CONNECT ON ENDPOINT::DIAG_EP TO [InstanceX_User];
   GO
   ```

14. 基になる証明書とエンドポイントのセキュリティが構成されたら、指定した方法を使用して、可用性グループを作成します。 セカンダリの初期化に使用するバックアップを手動でバックアップ、コピー、および復元するか、または[自動シード処理](automatically-initialize-always-on-availability-group.md)を使用することをお勧めします。 セカンダリ レプリカを初期化するためのウィザードの使用には、サーバー メッセージ ブロック (SMB) ファイルが関係し、ドメインに参加していないワークグループ クラスターを使用する場合は動作しない可能性があります。
15. リスナーを作成する場合は、その名前と IP アドレスの両方が DNS に登録されていることを確認します。

### <a name="next-steps"></a>次の手順 

- [可用性グループ ウィザードの使用 (SQL Server Management Studio)](use-the-availability-group-wizard-sql-server-management-studio.md)

- [[新しい可用性グループ] ダイアログ ボックスの使用 (SQL Server Management Studio)](use-the-new-availability-group-dialog-box-sql-server-management-studio.md)
 
- [Transact-SQL での可用性グループの作成](create-an-availability-group-transact-sql.md)

<!--Image references-->
[1]: ./media/diag-wsfc-two-data-centers-same-domain.png
[2]: ./media/diag-workgroup-cluster-two-nodes-joined.png
[3]: ./media/diag-high-level-view-ag-standard-edition.png
[4]: ./media/diag-successful-dns-suffix.png 
