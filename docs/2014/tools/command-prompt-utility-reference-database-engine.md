---
title: コマンドプロンプトユーティリティリファレンス (データベースエンジン) |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfb77db3676c8df124b65199fb0b806755e550a1
ms.sourcegitcommit: b4962530f90234017073b3fdd2248936b2de4e69
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71077509"
---
# <a name="command-prompt-utility-reference-database-engine"></a>コマンド プロンプト ユーティリティ リファレンス (データベース エンジン)
  コマンド プロンプト ユーティリティを使用すると、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の操作のスクリプトを作成できます。 次の表は、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] に付属するコマンド プロンプト ユーティリティの一覧です。  
  
|**Utility**|**説明**|**インストール先**|  
|-----------------|---------------------|----------------------|  
|[bcp ユーティリティ](bcp-utility.md)|ユーザー指定の形式で、[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスとデータ ファイルとの間でデータをコピーします。|\<*ドライブ*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta ユーティリティ](dta/dta-utility.md)|作業負荷の分析、およびその作業負荷に対してサーバー パフォーマンスを最適化するための推奨物理デザイン構造の分析を行います。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec ユーティリティ](../integration-services/packages/dtexec-utility.md)|[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] パッケージを構成および実行します。 このコマンド プロンプト ユーティリティのユーザー インターフェイス バージョンは **DTExecUI** と呼ばれ、パッケージ実行ユーティリティが表示されます。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Encrypt](../integration-services/dtutil-utility.md)|SSIS パッケージを管理します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[配置ユーティリティを使用したモデル ソリューションの配置](https://docs.microsoft.com/analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility)|[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] プロジェクトを [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] のインスタンスに配置します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[osql ユーティリティ](osql-utility.md)|[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[profiler ユーティリティ](profiler-utility.md)|コマンド プロンプトから [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] を起動します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[RS.exe ユーティリティ &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] レポート サーバーを管理するために作成されたスクリプトを実行します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig ユーティリティ &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|レポート サーバー接続を構成します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt ユーティリティ &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|レポート サーバー上の暗号化キーを管理します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 アプリケーション](sqlagent90-application.md)|コマンド プロンプトから [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] エージェントを開始します。|\<ドライブ>:\Program Files\Microsoft SQL Server\\<*instance_name*>\MSSQL\Binn|  
|[sqlcmd ユーティリティ](sqlcmd-utility.md)|[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメント、システム プロシージャ、およびスクリプト ファイルをコマンド プロンプトで入力できるようになります。|\<*ドライブ*:>\Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag ユーティリティ](sqldiag-utility.md)|[!INCLUDE[msCoName](../includes/msconame-md.md)] カスタマー サポート サービス用の診断情報を収集します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship アプリケーション](sqllogship-application.md)|バックアップ、コピー、および復元ジョブを実行することなく、ログ配布構成のバックアップ、コピー、復元操作、および関連するクリーンアップ作業を行うために使用されます。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB ユーティリティ](sqllocaldb-utility.md)|プログラムの開発者を対象とした [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の実行モードです。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlmaint ユーティリティ](sqlmaint-utility.md)|以前のバージョンの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]で作成されたデータベース メンテナンス プランを実行します。|\<ドライブ >: Server\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
|[sqlps ユーティリティ](sqlps-utility.md)|PowerShell コマンドおよびスクリプトを実行します。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell プロバイダーおよびコマンドレットの読み込みと登録を行います。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr アプリケーション](sqlservr-application.md)|トラブルシューティングを行うために、コマンド プロンプトから [!INCLUDE[ssDE](../includes/ssde-md.md)] インスタンスを開始および停止します。|\<ドライブ >: Server\MSSQL12.MSSQLSERVER\MSSQL\Binn|  
|[Ssms ユーティリティ](../ssms/ssms-utility.md)|コマンド プロンプトから [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を起動します。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff ユーティリティ](tablediff-utility.md)|2 つのテーブルのデータを比較し、非収束について調査します。これは、レプリケーション トポロジのトラブルシューティングを行う場合に便利です。|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM (COM)|  
  
 **[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーにアクセスするには - [!INCLUDE[win8](../includes/win8-md.md)]**  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーは [!INCLUDE[msCoName](../includes/msconame-md.md)] 管理コンソール プログラムのスナップインであり、スタンドアロン プログラムではありません。そのため、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を実行している場合、[!INCLUDE[win8](../includes/win8-md.md)] 構成マネージャーはアプリケーションとして表示されません。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 構成マネージャーを開くには、**検索**チャームで、 **[アプリ]** の下に「**SQLServerManager12.msc**」([!INCLUDE[ssSQL14](../includes/sssql14-md.md)] の場合) または「**SQLServerManager11.msc**」([!INCLUDE[ssSQL11](../includes/sssql11-md.md)] の場合) と入力し、**Enter** キーを押します。  
  
## <a name="command-prompt-utilities-syntax-conventions"></a>コマンド プロンプト ユーティリティで使用する構文表記規則  
  
|**表記**|**使用目的**|  
|--------------------|------------------|  
|大文字|オペレーティング システム レベルで使用するステートメントと用語|  
|`monospace`|サンプルのコマンドとプログラム コード|  
|*斜体*|ユーザーが指定するパラメーター|  
|**太字**|示されたとおりに入力する必要があるコマンド、パラメーター、およびその他の構文|  
  
## <a name="see-also"></a>参照  
 [レプリケーション ディストリビューション エージェント](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [レプリケーション ログ リーダー エージェント](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [レプリケーション マージ エージェント](../relational-databases/replication/agents/replication-merge-agent.md)   
 [レプリケーション キュー リーダー エージェント](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
