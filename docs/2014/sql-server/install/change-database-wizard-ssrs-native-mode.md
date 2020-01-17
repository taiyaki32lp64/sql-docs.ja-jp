---
title: データベースの変更ウィザード (SSRS ネイティブモード) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.changedatabase.F1
helpviewer_keywords:
- Change Database Wizard
- report server database, create
ms.assetid: 1a2e8d18-5997-482f-a9c1-87d99f7407b8
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: cd81004765b1ba5d15c5929dc661ce1dea04b371
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952662"
---
# <a name="change-database-wizard-ssrs-native-mode"></a>データベースの変更ウィザード (SSRS ネイティブ モード)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーのデータベースの変更ウィザードを使用して、新しいレポート サーバー データベースを作成するか、現在のレポート サーバー インスタンスで使用する既存のレポート サーバー データベースを選択することができます。  
  
 以前のバージョンのレポート サーバー データベースを選択すると、接続先のレポート サーバー インスタンスのバージョンと一致するようにアップグレードされます。 サービスの開始時にデータベース バージョンが確認され、現在のスキーマに自動的にアップグレードされます。  
  
 このウィザードを起動するには、 **構成マネージャーの [データベース] ページにある** [データベースの変更] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] をクリックします。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager を開始する方法の手順については、「[ネイティブモード&#40;&#41;の Reporting Services Configuration Manager](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md)」を参照してください。  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード。  
  
## <a name="options"></a>および  
 **操作**  
 実行するタスクを選択します。 ネイティブ モードまたは SharePoint 統合モードで新しいデータベースを作成できます。 または、現在のレポート サーバー インスタンスで使用する既存のレポート サーバー データベースを選択できます。  
  
 **データベースサーバー**  
 レポート サーバー データベースをホストする [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンス名を指定します。 ローカルまたはリモートのコンピューターの、既定または名前付きのインスタンスを使用できます。 名前付きインスタンスに接続する場合は、\<*server*>\\<*インスタンス*> の形式でサーバー名を入力します。  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] インスタンスに接続するには、サーバーにログオンしてデータベース情報を更新するための権限がある資格情報を使用する必要があります。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、現在の Windows 資格情報が使用されますが、ログイン権限またはデータベース権限がない場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ログインを指定する必要があります。 別の Windows 資格情報を指定することはできません。 別の Windows ユーザーとして接続する場合は、ユーザーとしてログインし、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーを起動します。  
  
 リモート インスタンスに接続する場合は、まずそのインスタンスでリモート接続を有効にする必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンおよびエディションの中には、既定でリモート接続が有効になっていないものもあります。 リモート接続が許可されているかどうかを確認するには、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 構成マネージャーを使用して、TCP/IP プロトコルおよび名前付きパイプ プロトコルが有効になっていることを確認します。 リモート インスタンスが名前付きインスタンスの場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser サービスが有効になっていることと、ターゲット サーバーで実行されていることを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser によって、名前付きインスタンスで使用されるポート番号が [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーに提供されます。  
  
 **データベース**  
 サーバー データを格納するレポート サーバー データベースの名前を指定します。 既存のデータベースを指定するか、新しいデータベースを作成できます。  
  
 [アクション] ページで **[新しいデータベースを作成する]** を選択すると、新しいデータベースの作成に使用されるプロパティがウィザードに表示されます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーは、名前でバインドされた 2 つのデータベースを作成します。1 つは静的データを格納するデータベースで、もう 1 つはセッションおよび作業データを格納するための一時データベースです。 詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンラインブックの「[レポートサーバーデータベース&#40;の SSRS ネイティブモード&#41; ](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md) 」を参照してください。  
  
 既存のレポート サーバー データベースを選択することもできます。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 構成マネージャーでは、無効なデータベースが除外されません。 有効なデータベースは、レポート サーバー データベース スキーマに基づきます (必要なテーブル、ビュー、またはストアド プロシージャが欠落しているデータベースは選択できません)。 以前のバージョンの [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]用に作成されたデータベースを選択すると、データベースが現在の形式にアップグレードされます。  
  
 **[言語]**  
 この値は、新しいレポート サーバー データベースを作成する場合にのみ設定します。  
  
 この値を使用して、ロールの定義および説明を作成するときの言語を指定します。 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] には、一連の定義済みロールを含んでいるロールベースの承認モデルが用意されています。 ロールは、指定した言語で一度だけ作成されます。 サーバーでサポートされているカルチャまたは言語が設定されているブラウザーを使用してレポート サーバーに接続した場合でも、ロール名と説明が指定以外の言語で表示されることはありません。 また、指定した言語によって、個人用レポート機能に含まれている [個人用レポート] フォルダーおよび [Users] フォルダーの名前の作成に使用される言語も決定されます。  
  
 **サーバーモード**  
 レポート サーバー データベースでは、ネイティブ モードまたは SharePoint 統合モードのいずれかがサポートされます。 これらのモードは、同時には指定できません。  
  
 新しいレポート サーバー データベースを作成する場合は、モードを指定する必要があります。 選択したモードにより、レポート サーバー データベースの構造が決まり、`SharePointIntegrated` レポート サーバー システム プロパティが `true` または `false` に設定されます。  
  
 別のレポート サーバー データベースを選択する場合は、現在のデータベースの使用方法がわかるように、現在のデータベースのモードが表示されます。  
  
 **[資格情報]**  
 レポート サーバーがレポート サーバー データベースへの接続に使用するアカウントを指定します。 指定できる値は、レポート サーバー Web サービスのサービス アカウント、レポート サーバーのホストに使用している [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスで定義されている [!INCLUDE[ssDE](../../includes/ssde-md.md)] データベース ログイン、または Windows アカウントです。 Windows アカウントを使用している場合は、レポートサーバーとデータベースが同じコンピューター上に存在する場合はローカルアカウント ( *\<computername >\\< username\>* ) を指定できます。同じドメイン内の異なるコンピューター上にある場合は、ドメインユーザーアカウント ( *\<ドメイン >\\ユーザー名 <* ) を指定できます。\>  
  
 レポート サーバーはデータベース ログインを作成し、指定したアカウントにデータベース権限を割り当てます。  
  
 レポート サーバーでは、アカウントの作成は行われません。 配置構成に対して有効な、既に存在するアカウントを指定する必要があります。 特に、データベースがリモート コンピューター上にある環境で、Windows アカウントを使用する場合は、そのコンピューターへのログオン権限のあるアカウントを指定する必要があります。  
  
 コンピューターが別のドメインまたは信頼されていないドメイン内に存在する場合は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース ログインを使用することをお勧めします。 アカウントの選択の詳細については、「[レポートサーバーデータベース接続&#40;の構成&#41;SSRS Configuration Manager](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)」を参照してください。  
  
 **概要**  
 セットアップで接続を構成する前に、設定を確認します。  
  
 **進行状況と完了**  
 各タスクの進行状況を監視します。  
  
## <a name="see-also"></a>参照  
 [データベース&#40;SSRS ネイティブモード&#41; ](../../../2014/sql-server/install/database-ssrs-native-mode.md)   
 [資格情報の&#40;変更ウィザード SSRS&#41;ネイティブモード](../../../2014/sql-server/install/change-credentials-wizard-ssrs-native-mode.md)   
 [ネイティブ モード レポート サーバー データベースの作成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md)   
 [Reporting Services Configuration Manager の F1 ヘルプ&#40;トピック SSRS ネイティブ&#41;モード](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [レポート サーバー データベース接続の構成 &#40;SSRS構成マネージャー&#41;](../../../2014/sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)  
  
  
