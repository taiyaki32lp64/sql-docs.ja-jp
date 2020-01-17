---
title: Integration Services のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
manager: erikre
ms.openlocfilehash: 0b7fd8a71f2636893f157b18630e2773b2f01951
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262791"
---
# <a name="upgrade-integration-services"></a>Integration Services のアップグレード

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降がコンピューターに現在インストールされている場合は、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]にアップグレードできます。  
  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] の以前のバージョンのいずれかがインストールされているコンピューターで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] にアップグレードすると、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は以前のバージョンに対してサイド バイ サイドでインストールされます。  
  
 このサイド バイ サイド インストールで、複数のバージョンの dtexec ユーティリティがインストールされます。 正しいバージョンのユーティリティを実行していることを確認するには、コマンド プロンプトで完全なパス (\<ドライブ>:\Program Files\Microsoft SQL Server\\<バージョン\>\DTS\Binn) を入力してユーティリティを実行します。 dtexec の詳細については、「 [dtexec Utility](../../integration-services/packages/dtexec-utility.md)」を参照してください。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールすると、既定で Users グループの全ユーザーが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできました。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]をインストールした場合、ユーザーは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできません。 このサービスは既定で保護されます。 特定のユーザーに対して [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サービスへのアクセスを許可するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールした後で DCOM 構成ツール (Dcomcnfg.exe) を実行する必要があります。 詳細については、「[Integration Services サービス (SSIS サービス)](../../integration-services/service/integration-services-service-ssis-service.md)」を参照してください。  
  
## <a name="before-upgrading-integration-services"></a>Integration Services をアップグレードする前に  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする前に、アップグレード アドバイザーを実行することをお勧めします。 アップグレード アドバイザーは、既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で使用される新しいパッケージ形式に移行する場合に発生する可能性がある問題を報告します。  
  
> [!NOTE]
>  SQL Server 2012 では、データ変換サービス (DTS) パッケージの移行または実行のサポートは廃止されました。 次の DTS 機能は廃止されました。  
> 
>  -   DTS ランタイム  
> -   DTS API  
> -   DTS パッケージを次期バージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   DTS パッケージのメンテナンス機能のサポート [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   DTS 2000 パッケージ実行タスク  
> -   アップグレード アドバイザーによる DTS パッケージのスキャン  
> 
>  廃止されたその他の機能については、「 [SQL Server 2016 で提供が中止された Integration Services の機能](https://msdn.microsoft.com/library/5ee40ceb-37b9-47a9-b90d-ce1de74b10f7)」をご覧ください。  
  
## <a name="upgrading-integration-services"></a>Integration Services のアップグレード  
 次の方法のいずれかを使用してアップグレードできます。  
  
-   [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] セットアップを実行し、 **[SQL Server 2008、SQL Server 2008 R2、[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、または [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] からのアップグレード]** を選択します。  
  
-   コマンド プロンプトで **setup.exe** を実行し、 **/ACTION=upgrade** オプションを指定します。 詳細については、「[コマンド プロンプトからの SQL Server 2016 のインストール](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)」の「[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインストール スクリプト」セクションを参照してください。  
  
 アップグレードでは、次の操作は実行できません。  
  
-   既にインストールされている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の再構成  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット版から 64 ビット版への移動または 64 ビット版から 32 ビット版への移動  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカライズ版どうしの間での移動  
  
 アップグレード時には、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)]の両方をアップグレードするか、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のみ、または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のみをアップグレードすることができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のみをアップグレードすると、 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降は引き続き機能しますが、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]の機能は使用できません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のみをアップグレードすると、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は完全に機能しますが、 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] のインスタンスを別のコンピューターで使用できない限り、パッケージを格納できる場所はファイル システムのみになります。  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Integration Services とデータベース エンジンの両方を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 ここでは、次の条件を満たしたアップグレードを実行した場合の影響について説明します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスをどちらも [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスがどちらも同じコンピューター上にある。  
  
### <a name="what-the-upgrade-process-does"></a>アップグレード プロセスで実行されるタスク  
 アップグレード プロセスでは次のタスクが行われます。  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] のファイル、サービス、およびツール ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] と [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]) をインストールします。 同じコンピューター上に [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] の複数のインスタンスが存在する場合は、どのインスタンスであっても、最初に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードするときに、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] のファイル、サービス、およびツールがインストールされます。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] バージョンにアップグレードします。  
  
-   次のように、 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降のシステム テーブルのデータを [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] システム テーブルに移動します。  
  
    -   パッケージを変更せずに msdb.dbo.sysdtspackages90 システム テーブルから msdb.dbo.sysssispackages システム テーブルに移動します。  
  
        > [!NOTE]  
        >  データは異なるシステム テーブルに移動されますが、アップグレード プロセスでは、パッケージは新しい形式には移行されません。  
  
    -   フォルダーのメタデータを msdb.sysdtsfolders90 システム テーブルから msdb.sysssisfolders システム テーブルに移動します。  
  
    -   ログ データを msdb.sysdtslog90 システム テーブルから msdb.sysssislog システム テーブルに移動します。  
  
-   新しい msdb.sysssis\* テーブルにデータを移動した後に、msdb.sysdts*90 システム テーブルとシステム テーブルへのアクセスに使用されるストアド プロシージャを削除します。 ただしアップグレードにより、sysdtslog90 テーブルは sysdtslog90 という名前のビューに置き換わります。 この新しい sysdtslog90 ビューでは、新しい msdb.sysssislog システム テーブルが公開されます。 これにより、ログ テーブルに基づいたレポートは、中断されることなく引き続き実行されます。  
  
-   パッケージへのアクセスを制御するために、db_ssisadmin、db_ssisltduser、および db_ssisoperator という 3 つの固定データベース レベル ロールを新しく作成します。 db_dtsadmin、db_dtsltduser、および db_dtsoperator という [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ロールは削除されませんが、対応する新しいロールのメンバーになります。  
  
-   [!INCLUDE[ssIS](../../includes/ssis-md.md)] パッケージ ストア ( [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスが管理するファイル システムの場所) が、 **\SQL Server\90**、 **\SQL Server\100**、 **\SQL Server\110**、 **\SQL Server\120** 内の既定の場所である場合、そのパッケージを新しい既定の場所である **\SQL Server\130**内に移動します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のアップグレード済みのインスタンスを指すように [!INCLUDE[ssDE](../../includes/ssde-md.md)]サービス構成ファイルを更新します。  
  
### <a name="what-the-upgrade-process-does-not-do"></a>アップグレード プロセスで実行されないタスク  
 アップグレード プロセスでは、次のタスクは行われません。  
  
-   **以降のサービスは** 削除されません [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 。  
  
-   既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で使用される新しいパッケージ形式に移行されません。 パッケージの移行方法については、「 [Integration Services パッケージのアップグレード](../../integration-services/install-windows/upgrade-integration-services-packages.md)」をご覧ください。  
  
-   パッケージは、サービス構成ファイルに追加されたファイル システムの場所からは移行されません。ただし、この場所が既定の場所である場合は移行できます。 既にサービス構成ファイルを編集してファイル システム フォルダーを追加している場合、追加したフォルダーに格納されているパッケージは新しい場所に移行されません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dtexec **ユーティリティ (dtexec.exe) を直接呼び出す** エージェント ジョブ ステップでは、 **dtexec** ユーティリティのファイル システム パスが更新されません。 これらのジョブ ステップを手動で編集し、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の **dtexec** ユーティリティの場所を指定するようにファイル システム パスを更新する必要があります。  
  
### <a name="what-you-can-do-after-upgrading"></a>アップグレード後に実行できるタスク  
 アップグレード プロセスが完了したら、次のタスクを実行できます。  
  
-   パッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行できます。  
  
-   [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] を使用して、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]のインスタンスに保存されている [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]パッケージを管理できます。 サービス構成ファイルを変更して、サービスによって管理される場所の一覧に [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] のインスタンスを追加する必要があります。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] サービス に接続することはできません。  
  
-   packageformat 列の値を確認することによって、msdb.dbo.sysssispackages システム テーブル内のパッケージのバージョンを識別できます。 このテーブルには、各パッケージのバージョンを識別する packageformat 列があります。 値 3 は、 [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] パッケージを示します。 パッケージを新しいパッケージ形式に移行するまで、packageformat 列の値は変わりません。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ツールを使用し、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージをデザイン、実行、管理することはできません。 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ツールには、各バージョンの [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード、パッケージ実行ユーティリティ (dtexecui.exe) などがあります。 アップグレード プロセスでは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]ツールは削除されません。 ただし、アップグレードしたサーバー上でこれらのツールを使用して、引き続き [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] 以降のパッケージで作業することはできません。  
  
-   既定では、アップグレード インストールで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はパッケージの実行に関連するイベントをアプリケーション イベント ログに記録するように構成されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のデータ コレクター機能を使用すると、この設定によって大量のイベント ログ エントリが生成される場合があります。 ログに記録されるイベントは、EventID 12288 の "パッケージが起動されました。" や EventID 12289 の "パッケージが正常に完了しました。" などです。 これら 2 つのイベントがアプリケーション イベント ログに記録されないようにするには、レジストリを編集用に開きます。 次に、レジストリ内で HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\130\SSIS ノードを見つけ、LogPackageExecutionToEventLog 設定の DWORD 値を 1 から 0 に変更します。  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>データベース エンジンのみを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 ここでは、次の条件を満たしたアップグレードを実行した場合の影響について説明します。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスのみをアップグレードする。 つまり、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のインスタンスであるが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインスタンスおよびクライアント ツールは [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、 [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]、 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]である状態。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] およびクライアント ツールとは別のコンピューター上にある。  
  
### <a name="what-you-can-do-after-upgrading"></a>アップグレード後に実行できるタスク  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のアップグレード済みのインスタンスのパッケージを格納するシステム テーブルは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]で使用されるシステム テーブルとは異なります。 したがって、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] バージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] および [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスのシステム テーブル内にあるパッケージは検出できません。 このため、これらのパッケージに対して実行できるタスクには制限があります。  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] および [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスのパッケージを読み込んだり管理したりする他のコンピューターでは使用できません。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../includes/ssde-md.md)] のアップグレード済みのインスタンスのパッケージはまだ新しいパッケージ形式に移行されていませんが、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールで検出することができません。 したがって、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールではこれらのパッケージを使用できません。  
  
-   [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] は、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスの msdb に格納されているパッケージを実行する他のコンピューターでは使用できません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のアップグレード済みのインスタンスに格納されている [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] パッケージを実行する [!INCLUDE[ssDE](../../includes/ssde-md.md)]コンピューターでは使用できません。  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ記事「 [既存のカスタムSSIS拡張機能とアプリケーションをデナリで動作させる](https://go.microsoft.com/fwlink/?LinkId=238157)」  
  
  
