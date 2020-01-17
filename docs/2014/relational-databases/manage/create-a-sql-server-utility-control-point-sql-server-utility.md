---
title: SQL Server ユーティリティ コントロール ポイントの作成 (SQL Server ユーティリティ) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.create.ucp.progress.F1
- SQL12.SWB.create.ucp.welcome.F1
- SQL12.SWB.create.ucp.Summary.F1
- SQL12.SWB.create.ucp.validation.F1
- SQL12.SWB.create.ucp.instancename.F1
- SQL12.SWB.create.ucp.agentconfiguration.F1
helpviewer_keywords:
- Create UCP
- UCP
ms.assetid: d5335124-1625-47ce-b4ac-36078967158c
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: db76db817561095b7b09b1a86e7c2ca10ec9174a
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798091"
---
# <a name="create-a-sql-server-utility-control-point-sql-server-utility"></a>SQL Server ユーティリティ コントロール ポイントの作成 (SQL Server ユーティリティ)
  企業では、複数の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティを所有することができ、各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティでは、多くの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスおよびデータ層アプリケーションを管理できます。 各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティには、ユーティリティ コントロール ポイント (UCP) を 1 つだけ含めることができます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティごとに新しい UCP を作成する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各マネージド インスタンス、および各データ層アプリケーション コンポーネントは、1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのみのメンバーであり、1 つの UCP で管理されます。  
  
 UCP では、15 分ごとに、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスから構成情報およびパフォーマンス情報を収集します。 情報は UCP のユーティリティ管理データ ウェアハウス (UMDW) に格納されます。UMDW ファイル名は sysutility_mdw です。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のパフォーマンス データはポリシーと比較され、リソース使用時のボトルネックおよび統合の可能性を特定するのに役立ちます。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 UCP を作成する前に、次の要件と推奨事項を確認してください。  
  
 このリリースでは、UCP および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのマネージド インスタンスが次の要件を満たしている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は Version 10.50 以上である必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスの型は [!INCLUDE[ssDE](../../includes/ssde-md.md)]であることが必要です。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティは、単一の Windows ドメイン、または双方向の信頼関係を持つドメイン間で操作する必要があります。  
  
-   SQL Server の UCP およびすべてのマネージド インスタンスの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] サービス アカウントには、Active Directory 内のユーザーに対する読み取り権限が必要です。  
  
 このリリースでは、UCP が次の要件を満たしている必要があります。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはサポートされているエディションである必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされている機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。  
  
-   UCP は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の大文字と小文字が区別されるインスタンスでホストすることをお勧めします。  
  
 UCP コンピューター上のキャパシティ プランニングについては、次の推奨事項を考慮してください。  
  
-   一般的なシナリオでは、UCP の UMDW データベース (sysutility_mdw) で使用されるディスク領域は、SQL Server のマネージド インスタンス 1 つにつき年間約 2 GB です。 この推定値は、マネージド インスタンスによって収集されるデータベース オブジェクトおよびシステム オブジェクトの数に応じて変化します。 UMDW (sysutility_mdw) のディスク領域の増加率は、最初の 2 日間で最大になります。  
  
-   一般的なシナリオでは、UCP の msdb に使用されるディスク領域は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のマネージド インスタンス 1 つにつき約 20 MB です。 この推定値は、リソース使用率のポリシーと、マネージド インスタンスによって収集されるデータベース オブジェクトおよびシステム オブジェクトの数に応じて変化します。 一般に、ポリシー違反の数が増加したり、変化しやすいリソースの移動期間が長くなるにつれて、使用されるディスク領域が増加します。  
  
-   UCP からマネージド インスタンスを削除しても、マネージド インスタンスのデータ保持期間の有効期限が切れるまでは、UCP のデータベースで使用されているディスク領域は縮小されません。  
  
 このリリースでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのマネージド インスタンスが次の要件を満たしている必要があります。  
  
-   UCP をホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスが大文字と小文字を区別しない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスでも大文字と小文字を区別しないことをお勧めします。  
  
-   FILESTREAM データは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの監視機能ではサポートされていません。  
  
 詳細については、 [SQL Server 2014 の各エディションがサポート](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)する SQL Server および機能[の最大容量仕様に](../../sql-server/maximum-capacity-specifications-for-sql-server.md)関する説明を参照してください。  
  
### <a name="remove-previous-utility-control-points-before-installing-a-new-one"></a>新しいユーティリティ コントロール ポイントをインストールする前に、以前のものを削除する  
 ユーティリティ コントロール ポイント (UCP) として構成されたことのある SQL Server インスタンスに UCP をインストールする場合、事前に SQL Server のすべてのマネージド インスタンスと UCP を削除しておく必要があります。 これには、 **sp_sysutility_ucp_remove** ストアド プロシージャを実行します。  
  
 このプロシージャは、次の要件を理解したうえで実行してください。  
  
-   このプロシージャは、UCP として構成されたコンピューターで実行する必要があります。  
  
-   このプロシージャは、sysadmin 権限を持つユーザーが実行する必要があります。この権限は、UCP の作成に必要な権限と同じです。  
  
-   SQL Server のマネージド インスタンスをすべて UCP から削除する必要があります。 UCP は、SQL Server のマネージド インスタンスの 1 つです。 詳細については、「 [SQL Server ユーティリティからの SQL Server のインスタンスの削除](https://go.microsoft.com/fwlink/?LinkId=169392)」を参照してください。  
  
 このプロシージャを使用して、SQL Server UCP を SQL Server ユーティリティから削除します。 操作の完了後は、この SQL Server インスタンスに再度 UCP を作成することができます。  
  
 UCP に接続するには、SQL Server Management Studio を使用して、次のスクリプトを実行します。  
  
```sql
EXEC msdb.dbo.sp_sysutility_ucp_remove;  
```  
  
> [!NOTE]  
>  UCP を削除した SQL Server インスタンスにユーティリティ以外のデータ コレクション セットがある場合、このプロシージャでは sysutility_mdw データベースが削除されません。 この場合、再度 UCP を作成するには、あらかじめ手動で sysutility_mdw データベースを削除しておく必要があります。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各マネージド インスタンス、および各データ層アプリケーション コンポーネントは、1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのみのメンバーであり、1 つの UCP で管理されます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの概念の詳細については、「 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)」を参照してください。  
  
 UCP は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの中心的な裏付けとなるポイントです。 UCP を使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データ層アプリケーションから収集された構成情報およびパフォーマンス情報を表示して、一般的なキャパシティ プランニングのアクティビティを実行できます。 UCP は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを登録および削除するための開始ポイントです。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録した後、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスとデータ層アプリケーションのリソースの正常性を監視して、統合の可能性を特定し、リソースのボトルネックを分離できます。 詳細については、「 [SQL Server ユーティリティでの SQL Server のインスタンスの監視](monitor-instances-of-sql-server-in-the-sql-server-utility.md)」を参照してください。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ以外のコレクション セットとサイド バイ サイドで実行できます。 つまり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのメンバーであれば、他のコレクション セットによって監視できます。 ただし、マネージド インスタンス上のすべてのコレクション セットは、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ管理データ ウェアハウスにアップロードすることに注意してください。 詳細については、「[SQL Server の同じインスタンスでユーティリティ コレクション セットとユーティリティ以外のコレクション セットを実行する場合の考慮事項](run-utility-and-non-utility-collection-sets-on-same-sql-instance.md)」、および「[ユーティリティ コントロール ポイント データ ウェアハウスの構成 &#40;SQL Server Utility&#41;](configure-your-utility-control-point-data-warehouse-sql-server-utility.md)」を参照してください。  
  
## <a name="wizard-steps"></a>ウィザードの手順  
 ![](../../database-engine/media/create-ucp.gif "Create_UCP")  
  
 以降のセクションでは、新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP を作成するワーク フローで使用するウィザードの各ページについて説明します。 新しい UCP を作成するウィザードを起動するには、SSMS の [表示] メニューからユーティリティエクスプローラーのウィンドウを開き、 ![](../../database-engine/media/create-ucp.gif "Create_UCP")ユーティリティエクスプローラーのウィンドウ上部にある **[UCP の作成]** ボタンをクリックします。  
  
 次の一覧にあるリンクをクリックすると、ウィザードのページの詳細に移動できます。  
  
 この操作を実行する PowerShell スクリプトの詳細については、 [例](#PowerShell_create_UCP)を参照してください。  
  
-   [UCP の作成ウィザードの概要](#Welcome)  
  
-   [インスタンスの指定](#Instance_name)  
  
-   [接続ダイアログ](#Connection_dialog)  
  
-   [ユーティリティ コレクション セットのアカウント](#Agent_configuration)  
  
-   [検証規則](#Validation_rules)  
  
-   [概要](#Summary)  
  
-   [ユーティリティ コントロール ポイントの作成](#Creating_UCP)  
  
##  <a name="Welcome"></a> UCP の作成ウィザードの概要  
 ユーティリティ エクスプローラーを開いたときに、接続されたユーティリティ コントロール ポイントがない場合は、ユーティリティ コントロール ポイントに接続するか、新しいユーティリティ コントロール ポイントを作成する必要があります。  
  
 **既存の UCP に接続する**-配置に既にユーティリティコントロールポイントがある場合は、ユーティリティエクスプローラーのウィンドウ上部に![](../../database-engine/media/connect-to-utility.gif "Connect_to_Utility")ある **[ユーティリティへの接続]** ボタンをクリックして接続できます。 既存の UCP に接続するには、管理者資格情報を持っているか、Utility Reader ロールのメンバーである必要があります。 UCP は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティごとに 1 つだけ存在できます。また、1 つの SSMS インスタンスから接続できる UCP は 1 つだけです。  
  
 **新しい UCP を作成**する-新しいユーティリティコントロールポイントを作成するには![ ](../../database-engine/media/create-ucp.gif "Create_UCP")、ユーティリティエクスプローラーのウィンドウ上部にある **[ucp の作成]** ボタンをクリックします。 新しい UCP を作成するには、接続ダイアログで、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名と管理者資格情報を指定する必要があります。 UCP は 1 つの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティにつき 1 つだけ存在します。  
  
##  <a name="Instance_name"></a> インスタンスの指定  
 作成する UCP について、次の情報を指定します。  
  
-   **インスタンス名**-接続ダイアログから [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスを選択するには、 **[接続]** をクリックします。Computername\instancename の形式で、コンピューター名と [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名を指定します。  
  
-   **ユーティリティ名** - ネットワーク上で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティを識別するために使用される名前を指定します。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Connection_dialog"></a> 接続ダイアログ  
 [サーバーへの接続] ダイアログ ボックスで、サーバーの種類、コンピューター名、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンス名の情報を確認します。 詳細については、「[サーバーへの接続 &#40;データベース エンジン&#41;](../../ssms/f1-help/connect-to-server-database-engine.md)」を参照してください。  
  
> [!NOTE]  
>  接続が暗号化されている場合、暗号化された接続が使用されます。 接続が暗号化されていない場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティは暗号化された接続を使用して再接続します。  
  
 続行するには、 **[接続]** をクリックします。  
  
##  <a name="Agent_configuration"></a> ユーティリティ コレクション セットのアカウント  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットを実行する Windows ドメイン アカウントを指定します。 このアカウントは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントとして使用されます。 また、既存の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントを使用することもできます。 検証の要件を満たすには、次のガイドラインに従ってアカウントを指定します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントのオプションを指定する場合は、次のガイドラインに従います。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントには、ビルトイン アカウント (LocalSystem、NetworkService、LocalService など) ではなく、Windows ドメイン アカウントを指定する必要があります。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Validation_rules"></a> 検証規則  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のこのリリースでは、UCP が作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで、次の条件が満たされている必要があります。  
  
|検証規則|修正措置|  
|---------------------|-----------------------|  
|ユーティリティ コントロール ポイントが作成される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスに対する管理者特権が必要です。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスに対する管理者特権を持つアカウントでログオンします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンは 10.50 以上である必要があります。|UCP をホストする別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスはサポートされているエディションである必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされている機能の一覧については、「 [SQL Server 2014 の各エディションがサポートする機能](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)」を参照してください。|UCP をホストする別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに、別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UCP に登録されている [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは指定できません。|異なる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定して UCP をホストするか、現在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のマネージド インスタンスである UCP から [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの登録を解除します。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスは既にユーティリティ コントロール ポイントをホストしていてはいけません。|UCP をホストする別の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスを指定します。|  
|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで TCP/IP を有効にする必要があります。|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスの TCP/IP を有効にします。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでは、データベースに "sysutility_mdw" という名前を付けることはできません。|UCP を作成する操作により、"sysutility_mdw" という名前のユーティリティ管理データ ウェアハウス (UMDW) が作成されます。 この操作では、検証規則の実行時にこの名前がコンピューター上に存在しないようにする必要があります。 続行するには、"sysutility_mdw" という名前のデータベースを削除するか、その名前を変更する必要があります。 名前変更操作の詳細については、「[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)」を参照してください。|  
|指定された [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスのコレクション セットを停止する必要があります。|指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンスで UCP が作成されている間は、既存のコレクション セットを停止します。 データ コレクターが無効になっている場合は、それを有効にして、実行中のコレクション セットを停止し、UCP の作成操作に対して検証規則を再実行します。<br /><br /> データ コレクターを有効にするには :<br /><br /> オブジェクト エクスプローラーで、 **[管理]** ノードを展開します。<br /><br /> **[データ コレクション]** を右クリックし、 **[データ コレクションの有効化]** をクリックします。<br /><br /> コレクション セットを停止するには :<br /><br /> オブジェクト エクスプローラーで、[管理] ノード、 **[データ コレクション]** 、 **[システム データ コレクション セット]** の順に展開します。<br /><br /> 停止するコレクション セットを右クリックして **[データ コレクション セットの停止]** をクリックします。<br /><br /> メッセージ ボックスにはこのアクションの結果が表示され、コレクション セットのアイコンに赤い丸が付いている場合は、コレクション セットが停止していることを示します。|  
|指定したインスタンスで [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始する必要があります。 指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインスタンスである場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを手動で開始するように構成する必要があります。 それ以外の場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが自動的に開始されるように構成する必要があります。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを開始します。 指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスが [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] フェールオーバー クラスターのインスタンスである場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスを手動で開始するように構成します。 それ以外の場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービスが自動的に開始されるように構成します。|  
|WMI が正しく構成されている必要があります。|WMI の構成をトラブルシューティングするには、「 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)」を参照してください。|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントには、ビルトイン アカウント (Network Service など) を使用できません。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントがビルトイン アカウント (Network Service など) の場合は、Windows ドメイン アカウント sysadmin にアカウントを再割り当てします。|  
|プロキシ アカウント オプションを選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント プロキシ アカウントが Windows ドメインの有効なアカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログオンします。|  
|サービス アカウント オプションを選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントにビルトイン アカウント (Network Service など) を使用できません。|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントがビルトイン アカウント (Network Service など) の場合は、Windows ドメイン アカウントにアカウントを再割り当てします。|  
|サービス アカウント オプションを選択した場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス アカウントは Windows ドメインの有効なアカウントである必要があります。|有効な Windows ドメイン アカウントを指定します。 アカウントが有効であることを確認するには、Windows ドメイン アカウントを使用して、指定した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにログオンします。|  
  
 検証結果に失敗した条件が示されている場合は、支障をきたす問題を解決した後、 **[検証の再実行]** をクリックして、コンピューターの構成を確認します。  
  
 検証レポートを保存するには、 **[レポートの保存]** をクリックし、ファイルの場所を指定します。  
  
 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Summary"></a> 概要  
 概要ページには、UCP について指定した情報が表示されます。  
  
-   UCP をホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスの名前。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティの名前。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティのデータ収集に対してジョブを実行するために使用されるアカウントの名前。  
  
 UCP 構成設定を変更するには、 **[前へ]** をクリックします。 続行するには、 **[次へ]** をクリックします。  
  
##  <a name="Creating_UCP"></a> ユーティリティ コントロール ポイントの作成  
 UCP の作成操作中は、ウィザードに手順と進行状況が表示されます。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで UCP を作成する準備をしています。  
  
-   ユーティリティ管理データ ウェアハウス (UMDW) を作成しています。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] UMDW を初期化しています。UMDW ファイル名は sysutility_mdw です。  
  
-   UCP を構成しています。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ コレクション セットを構成しています。  
  
 UCP の作成操作に関するレポートを保存するには、 **[レポートの保存]** をクリックし、ファイルの場所を指定します。  
  
 ウィザードを完了するには、 **[完了]** をクリックします。  
  
 UCP の作成ウィザードを完了すると、SSMS のユーティリティ エクスプローラーのナビゲーション ウィンドウでは、UCP のノードが表示され、その下に、配置済みのデータ層アプリケーション、マネージド インスタンス、およびユーティリティ管理のノードが表示されます。 UCP は自動的にマネージド インスタンスになります。  
  
 データ収集プロセスはすぐに開始されますが、ユーティリティ エクスプローラーのコンテンツ ウィンドウ内のダッシュボードとビューポイントに最初に表示されるまで最大 30 分かかる場合があります。 データの収集は 15 分間隔で続行されます。 初期データは UCP 自体から取得されます。 つまり、UCP は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティにおいて、最初の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] マネージド インスタンスです。  
  
 ダッシュボードを表示するには、SSMS のメニューで **[表示]** をクリックし、 **[ユーティリティ エクスプローラーのコンテンツ]** をクリックします。 データを更新するには、ユーティリティ エクスプローラーのウィンドウでユーティリティ名を右クリックし、 **[更新]** をクリックします。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の追加のインスタンスを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティに登録する方法については、「[SQL Server のインスタンスの登録 (SQL Server ユーティリティ)](enroll-an-instance-of-sql-server-sql-server-utility.md)」を参照してください。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティからマネージド インスタンスである UCP を削除するには、 **ユーティリティ エクスプローラー** のウィンドウで **[マネージド インスタンス]** を選択してマネージド インスタンスのリスト ビューを設定し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ユーティリティ エクスプローラー **のコンテンツ ウィンドウのリスト ビューで** インスタンス名を右クリックして、 **[マネージド インスタンスを削除]** を選択します。  
  
##  <a name="PowerShell_create_UCP"></a> PowerShell を使用したユーティリティ コントロール ポイントの新規作成  
 次の例を使用すると、新しいユーティリティ コントロール ポイントを作成できます。  
  
```powershell
$UtilityInstance = new-object -Type Microsoft.SqlServer.Management.Smo.Server "ComputerName\UCP-Name";  
$SqlStoreConnection = new-object -Type Microsoft.SqlServer.Management.Sdk.Sfc.SqlStoreConnection $UtilityInstance.ConnectionContext.SqlConnectionObject;  
$Utility = [Microsoft.SqlServer.Management.Utility.Utility]::CreateUtility("Utility", $SqlStoreConnection, "ProxyAccount", "ProxyAccountPassword");  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server ユーティリティの機能とタスク](sql-server-utility-features-and-tasks.md)   
 [SQL Server ユーティリティのトラブルシューティング](../../database-engine/troubleshoot-the-sql-server-utility.md)  
