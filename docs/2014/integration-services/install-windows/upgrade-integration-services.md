---
title: Integration Services のアップグレード | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: d1e40954a5a5eb7a69ba4f70b798356f38175fed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62768088"
---
# <a name="upgrade-integration-services"></a>Integration Services のアップグレード
  [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] または [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] がコンピューターに現在インストールされている場合は、[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] にアップグレードできます。  
  
 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] の以前のバージョンのいずれかがインストールされているコンピューターで [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] にアップグレードすると、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は以前のバージョンに対してサイド バイ サイドでインストールされます。  
  
 このサイド バイ サイド インストールで、複数のバージョンの dtexec ユーティリティがインストールされます。 正しいバージョンのユーティリティを実行していることを確認するには、コマンド プロンプトで完全なパス (\<ドライブ>:\Program Files\Microsoft SQL Server\\<バージョン\>\DTS\Binn) を入力してユーティリティを実行します。 dtexec の詳細については、「 [dtexec Utility](../packages/dtexec-utility.md)」を参照してください。  
  
> [!NOTE]  
>  以前のバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をインストールすると、既定で Users グループの全ユーザーが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできました。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]をインストールした場合、ユーザーは [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] サービスにアクセスできません。 このサービスは既定で保護されます。 特定のユーザーに対して [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] サービスへのアクセスを許可するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理者が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] をインストールした後で DCOM 構成ツール (Dcomcnfg.exe) を実行する必要があります。 詳細については、「 [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md)」を参照してください。  
  
## <a name="before-upgrading-integration-services"></a>Integration Services をアップグレードする前に  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする前に、アップグレード アドバイザーを実行することをお勧めします。 アップグレード アドバイザーは、既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で使用される新しいパッケージ形式に移行する場合に発生する可能性がある問題を報告します。 詳細については、「 [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)」を参照してください。  
  
> [!NOTE]
>  現在のリリースでの移行またはデータ変換サービス (DTS) パッケージの実行のサポートは廃止されました[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]します。 次の DTS 機能は廃止されました。  
> 
>  -   DTS ランタイム  
> -   DTS API  
> -   DTS パッケージを次期バージョンの [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   DTS パッケージのメンテナンス機能のサポート [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   DTS 2000 パッケージ実行タスク  
> -   アップグレード アドバイザーによる DTS パッケージのスキャン  
> 
>  その他の提供が中止された機能については、次を参照してください。[提供が中止された Integration Services の機能で SQL Server 2014](../discontinued-integration-services-functionality-in-sql-server-2014.md)します。  
  
## <a name="upgrading-integration-services"></a>Integration Services のアップグレード  
 次の方法のいずれかを使用してアップグレードできます。  
  
-   実行[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]セットアップするオプションを選択および**SQL Server 2005、SQL Server 2008 または SQL Server 2008 R2 からアップグレード**、または **[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]** します。  
  
-   実行**setup.exe**コマンド プロンプトで指定し、`/ACTION=upgrade`オプション。 詳細については、このセクションを参照してください。"インストール スクリプト」 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]、"で[コマンド プロンプトから SQL Server 2014 のインストール](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)します。  
  
 アップグレードでは、次の操作は実行できません。  
  
-   既にインストールされている [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]の再構成  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 32 ビット版から 64 ビット版への移動または 64 ビット版から 32 ビット版への移動  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のローカライズ版どうしの間での移動  
  
 アップグレード時には、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)]の両方をアップグレードするか、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のみ、または [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のみをアップグレードすることができます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のみをアップグレードすると、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] または [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] は引き続き機能しますが、[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] の機能は使用できません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のみをアップグレードすると、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] は完全に機能しますが、 [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] のインスタンスを別のコンピューターで使用できない限り、パッケージを格納できる場所はファイル システムのみになります。  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Integration Services とデータベース エンジンの両方を [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 ここでは、次の条件を満たしたアップグレードを実行した場合の影響について説明します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスをどちらも [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]にアップグレードする。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] と [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスがどちらも同じコンピューター上にある。  
  
### <a name="what-the-upgrade-process-does"></a>アップグレード プロセスで実行されるタスク  
 アップグレード プロセスでは次のタスクが行われます。  
  
-   [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] のファイル、サービス、およびツール ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] と [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]) をインストールします。 同じコンピューター上に [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] の複数のインスタンスが存在する場合は、どのインスタンスであっても、最初に [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] にアップグレードするときに、[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] のファイル、サービス、およびツールがインストールされます。  
  
-   インスタンスをアップグレード、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]または[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]を[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]バージョン。  
  
-   データを移動、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]または[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]システム テーブル、[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]システム テーブルに次のようにします。  
  
    -   パッケージを変更せずに msdb.dbo.sysdtspackages90 システム テーブルから msdb.dbo.sysssispackages システム テーブルに移動します。  
  
        > [!NOTE]  
        >  データは異なるシステム テーブルに移動されますが、アップグレード プロセスでは、パッケージは新しい形式には移行されません。  
  
    -   フォルダーのメタデータを msdb.sysdtsfolders90 システム テーブルから msdb.sysssisfolders システム テーブルに移動します。  
  
    -   ログ データを msdb.sysdtslog90 システム テーブルから msdb.sysssislog システム テーブルに移動します。  
  
-   新しい msdb.sysssis\* テーブルにデータを移動した後に、msdb.sysdts\*90 システム テーブルとシステム テーブルへのアクセスに使用されるストアド プロシージャを削除します。 ただしアップグレードにより、sysdtslog90 テーブルは sysdtslog90 という名前のビューに置き換わります。 この新しい sysdtslog90 ビューでは、新しい msdb.sysssislog システム テーブルが公開されます。 これにより、ログ テーブルに基づいたレポートは、中断されることなく引き続き実行されます。  
  
-   パッケージへのアクセスを制御するために、db_ssisadmin、db_ssisltduser、および db_ssisoperator という 3 つの固定データベース レベル ロールを新しく作成します。 db_dtsadmin、db_dtsltduser、および db_dtsoperator という [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ロールは削除されませんが、対応する新しいロールのメンバーになります。  
  
-   場合、[!INCLUDE[ssIS](../../includes/ssis-md.md)]パッケージ ストア (で管理されているファイル システムの場所は、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]サービス) が既定の場所で **\SQL Server\90**、 **\SQL Server\100**、または **\SQL Server\110**下で新しい既定の場所にそれらのパッケージを移動 **\SQL Server\120**します。  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のアップグレード済みのインスタンスを指すように [!INCLUDE[ssDE](../../includes/ssde-md.md)]サービス構成ファイルを更新します。  
  
### <a name="what-the-upgrade-process-does-not-do"></a>アップグレード プロセスで実行されないタスク  
 アップグレード プロセスでは、次のタスクは行われません。  
  
-   **いない**削除、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]または[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]サービス。  
  
-   既存の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で使用される新しいパッケージ形式に移行されません。 パッケージの移行方法については、「 [Integration Services パッケージのアップグレード](upgrade-integration-services-packages.md)」をご覧ください。  
  
-   パッケージは、サービス構成ファイルに追加されたファイル システムの場所からは移行されません。ただし、この場所が既定の場所である場合は移行できます。 既にサービス構成ファイルを編集してファイル システム フォルダーを追加している場合、追加したフォルダーに格納されているパッケージは新しい場所に移行されません。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dtexec **ユーティリティ (dtexec.exe) を直接呼び出す** エージェント ジョブ ステップでは、 **dtexec** ユーティリティのファイル システム パスが更新されません。 これらのジョブ ステップを手動で編集し、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] の **dtexec** ユーティリティの場所を指定するようにファイル システム パスを更新する必要があります。  
  
### <a name="what-you-can-do-after-upgrading"></a>アップグレード後に実行できるタスク  
 アップグレード プロセスが完了したら、次のタスクを実行できます。  
  
-   パッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを実行できます。  
  
-   使用[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]を管理する[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]のインスタンスに格納されているパッケージ[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]または[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]します。 サービス構成ファイルを変更して、サービスによって管理される場所の一覧に [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] のインスタンスを追加する必要があります。  
  
    > [!NOTE]  
    >  以前のバージョンの [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] では、 [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] サービス に接続することはできません。  
  
-   packageformat 列の値を確認することによって、msdb.dbo.sysssispackages システム テーブル内のパッケージのバージョンを識別できます。 このテーブルには、各パッケージのバージョンを識別する packageformat 列があります。 packageformat 列の値が 2 の場合は、[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] パッケージであることを示します。値が 3 の場合は、[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] パッケージであることを示します。 パッケージを新しいパッケージ形式に移行するまで、packageformat 列の値は変わりません。  
  
-   使用することはできません、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]または[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]デザイン、実行、または管理するためのツール[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]パッケージ。 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ツールおよび [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールには、各バージョンの [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザード、パッケージ実行ユーティリティ (dtexecui.exe) などがあります。 アップグレード プロセスは削除されません、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]または[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]ツール。 ただし、アップグレードしたサーバー上でこれらのツールを使用して、引き続き [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] パッケージまたは [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] パッケージで作業することはできません。  
  
-   既定では、アップグレード インストールで、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] はパッケージの実行に関連するイベントをアプリケーション イベント ログに記録するように構成されます。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]のデータ コレクター機能を使用すると、この設定によって大量のイベント ログ エントリが生成される場合があります。 ログに記録されるイベントは、EventID 12288 の "パッケージが起動されました。" や EventID 12289 の "パッケージが正常に完了しました。" などです。 これら 2 つのイベントがアプリケーション イベント ログに記録されないようにするには、レジストリを編集用に開きます。 次に、レジストリ内で HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS ノードを見つけ、LogPackageExecutionToEventLog 設定の DWORD 値を 1 から 0 に変更します。  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>データベース エンジンのみを [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 ここでは、次の条件を満たしたアップグレードを実行した場合の影響について説明します。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスのみをアップグレードする。 つまり、[!INCLUDE[ssDE](../../includes/ssde-md.md)]は [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] のインスタンスであるが、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のインスタンスおよびクライアント ツールは [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] である状態。  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスが、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] およびクライアント ツールとは別のコンピューター上にある。  
  
### <a name="what-you-can-do-after-upgrading"></a>アップグレード後に実行できるタスク  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスのパッケージを格納するシステム テーブルは、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] または [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] で使用されるシステム テーブルとは異なります。 そのため、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]または[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]のバージョンの[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]と[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]のアップグレード済みのインスタンスのシステム テーブル内のパッケージを検出することはできません、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。 このため、これらのパッケージに対して実行できるタスクには制限があります。  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ツールまたは [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツール、[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]、および [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] は、[!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスのパッケージを読み込んだり管理したりするコンピューターに対しては使用できません。  
  
    > [!NOTE]  
    >  [!INCLUDE[ssDE](../../includes/ssde-md.md)]のアップグレード済みのインスタンスのパッケージはまだ新しいパッケージ形式に移行されていませんが、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ツールまたは [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールで検出することはできません。 したがって、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ツールまたは [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ツールではこれらのパッケージを使用できません。  
  
-   使用することはできません[!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]または[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]のアップグレードされたインスタンス上の msdb に格納されているパッケージを実行するには、他のコンピューターで、[!INCLUDE[ssDE](../../includes/ssde-md.md)]します。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブは、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]のアップグレード済みのインスタンスに格納されている [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] パッケージまたは [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] パッケージを実行する [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] コンピューターまたは [!INCLUDE[ssDE](../../includes/ssde-md.md)] コンピューターでは使用できません。  
  
## <a name="external-resources"></a>外部リソース  
 blogs.msdn.com のブログ記事「 [既存のカスタムSSIS拡張機能とアプリケーションをデナリで動作させる](https://go.microsoft.com/fwlink/?LinkId=238157)」  
  
  
