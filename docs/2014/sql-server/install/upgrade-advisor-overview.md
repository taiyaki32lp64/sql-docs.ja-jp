---
title: アップグレード アドバイザーの概要 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c78630764a26bb8fe281446c1bb997f18d965db7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091594"
---
# <a name="upgrade-advisor-overview"></a>アップグレード アドバイザーの概要
  アップグレード アドバイザーには、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]、[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、および [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] のコンポーネントを分析し、分析結果に関する情報が記載されたレポートを表示するための中央コンソールが用意されています。  
  
## <a name="how-upgrade-advisor-works"></a>アップグレード アドバイザーの機能  
 アップグレード アドバイザーを実行すると、アップグレード アドバイザーの開始ページが表示されます。 アップグレード アドバイザーの開始ページからは、以下を起動できます。  
  
-   アップグレード アドバイザー分析ウィザード  
  
-   アップグレード アドバイザー レポート ビューアー  
  
-   アップグレード アドバイザーのヘルプ  
  
 アップグレード アドバイザーを初めて使用するときは、アップグレード アドバイザー分析ウィザードを実行してサーバーを分析します。 ウィザードでは、分析が完了したら、クリックして**レポートの起動**ウィザードまたはアップグレード アドバイザーの開始ページに戻ります。 そこから、アップグレード アドバイザー レポート ビューアーを実行してレポートを表示します。 レポートには、既知の問題の解決に役立つ情報へのリンクが含まれています。  
  
## <a name="upgrade-advisor-analysis-wizard"></a>アップグレード アドバイザー分析ウィザード  
 分析を実行するには、次のようにクリックします。**アップグレード アドバイザー分析ウィザードを起動**アップグレード アドバイザーの開始ページです。 アップグレード アドバイザー分析ウィザードによって、分析するコンピューター、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンス、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント、およびトレース ファイルに関する情報が収集されます。 すべての情報の収集と確認が完了した後、アップグレード アドバイザー分析ウィザードによって [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントが分析されます。  
  
> [!NOTE]  
>  アップグレード アドバイザー分析ウィザードを実行するたびに個別のレポートが生成され、選択したコンポーネントに関する既存のレポートは上書きされません。 ただし、レポート ビューアーで表示されるのは、最近 5 件のレポートのみです。  
  
 アップグレード アドバイザー分析ウィザードによる分析が完了すると、分析対象として選択したコンポーネントごとに XML ファイルが作成されます。 これらの XML ファイルには、各コンポーネントの検出されたアイテムと問題が含まれています。  
  
### <a name="what-upgrade-advisor-analyzes"></a>アップグレード アドバイザーの分析対象  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のコンポーネントごとに、アップグレード アドバイザーのコンテキスト内で専用のアナライザーが実行されます。 各アナライザーは、コンポーネントに関する XML レポートを出力します。  
  
 アップグレード アドバイザーでは、次の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネントが照会されます。  
  
-   レプリケーション、[!INCLUDE[ssDE](../../includes/ssde-md.md)] エージェント、フルテキスト検索、および [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client を含むデータベース サーバー ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックでは[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]とも呼ばれます)  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  分析時に、各アナライザーによってログ ファイルが作成されます。 ログ ファイルを使用して、分析のトラブルシューティングを行うことができます。 たとえば、アップグレード アドバイザーの実行速度が遅い場合、ログ ファイルを表示して遅延の原因を突き止めることができます。  
  
### <a name="upgrade-advisor-limitations"></a>アップグレード アドバイザーの制限事項  
 アップグレード アドバイザーではアップグレードに影響するすべての問題を検出することはできません。 たとえば、エンド ユーザーのデスクトップで実行するクライアント アプリケーションに SQL コードを埋め込んだ場合は、アップグレード アドバイザーでそのアプリケーションを分析できません。 このようなアイテムに対しては、問題を検討し、インストールに必要な情報をアップグレード、移行、または修正する必要があります。  
  
 アップグレード アドバイザーで、暗号化されたストアド プロシージャ、拡張ストアド プロシージャのコード、および [!INCLUDE[tsql](../../includes/tsql-md.md)] 以外の言語によるソース コードの分析は行われません。  
  
## <a name="upgrade-advisor-report-viewer"></a>アップグレード アドバイザー レポート ビューアー  
 アップグレード アドバイザーのレポートを表示する をクリックして**アップグレード アドバイザー レポート ビューアーの起動**アップグレード アドバイザーの開始ページです。 アップグレード アドバイザー レポート ビューアーが起動し、既定ディレクトリのレポートが読み込まれます。 アップグレード アドバイザー レポート ビューアーでは、既定のディレクトリには、すべてのレポートが見つからない場合、レポートは表示されません。 既定ディレクトリにレポートがない場合は、アップグレード アドバイザー分析ウィザードを実行してレポートを作成するか、別のサーバーまたはサブディレクトリから既存のレポートを読み込みます。  
  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] アップグレード アドバイザーで、既存のレポートは上書きされません。 ただし、レポート ビューアーで表示されるのは、最近 5 件のレポートのみです。 以前のレポートを表示するからレポートを選択します。、**レポート**ドロップダウン リスト ボックス。 タイムスタンプにより、レポートが生成された日時が示されます。  
  
 XML ファイルがアップグレード アドバイザー分析ウィザードからアップグレード アドバイザー レポート ビューアーに読み込まれると、各コンポーネントのレポートが表示されます。 レポートには、対処が必要な既知の問題が検出できるできないに限らず、すべて含まれています。 各問題には、重要度を示すアイコン、問題の修正が必要な時期を示すラベル、および簡単な説明が付けられています。 問題を展開すると、より詳しい説明、問題の詳細へのリンク、およびヘルプ ファイルへのリンクが表示されます。 各問題の情報は、問題を修正するために十分な情報を提供するように設計されています。  
  
 ほとんどのコンポーネントには、検出できない問題があります。 これらの問題を表示するには、展開、**その他のアップグレードに関する問題**コンポーネントの項目し、ドキュメントの問題に関する追加情報を表示するリンクをクリックします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の下位互換性の問題の詳細については、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オンライン ブックを参照してください。  
  
## <a name="see-also"></a>参照  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
