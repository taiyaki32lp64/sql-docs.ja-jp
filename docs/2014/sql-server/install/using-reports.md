---
title: レポートの使用 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- overriding reports
- Upgrade Advisor Report Viewer
- reports [Upgrade Advisor], about reports
- formatting reports
- resolved issues [Upgrade Advisor]
- distributing reports [Reporting Services]
- filtering reports [Reporting Services]
- removing report items
- viewing reports
- rerunning analysis
- information issues [Upgrade Advisor]
- deleting report items
- icons [Upgrade Advisor]
- Upgrade Advisor [SQL Server], reports
- sending reports
- blocking issues [Upgrade Advisor]
- sharing reports
- reports [Upgrade Advisor]
- SQL Server Upgrade Advisor, reports
- modifying reports
- distributing reports [Reporting Services], about report distribution
- warnings [Upgrade Advisor]
- analyzing system [Upgrade Advisor], reports
ms.assetid: 4a3cb94a-a7ac-4cec-94c7-db26fcf6d161
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: fc3a08e707f6b51059145c69fdee15f78c933135
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66091229"
---
# <a name="using-reports"></a>レポートの使用
  アップグレード アドバイザー分析ウィザードによってサーバー上で分析されたコンポーネントごとまたはインスタンスごとに、個別のレポートが生成されます。 レポートでは、アップグレードに影響する既知の問題の詳細を参照できます。 情報と特定された問題に対処するための推奨されるアクションへのリンクも提供します。  
  
> [!NOTE]  
>  アップグレード アドバイザー レポート ビューアーが、既定のレポート ディレクトリにレポートを検索しない場合、別のディレクトリからのレポートを読み込むを使用して、**レポートを開く**リンク。  
  
## <a name="viewing-reports"></a>レポートの表示  
 アップグレード アドバイザー レポート ビューアーを使用して、アップグレード アドバイザー レポートを表示します。 レポートでは、アップグレード アドバイザーの開始ページを表示する をクリックして**アップグレード アドバイザー レポート ビューアーの起動**します。  
  
 サーバーのレポートを読み込んだ後、アップグレード問題を確認するコンポーネントを選択できます。 フィルターを適用することができます、**フィルターによって**ボックスに、次を参照してください。  
  
-   すべての問題  
  
-   アップグレードに関するすべての問題  
  
-   アップグレード前の問題  
  
-   移行に関するすべての問題  
  
-   解決した問題  
  
-   未解決の問題  
  
 クリックして問題の次または前のグループに移動することができます、レポートに 20 個を超える問題がある場合は、**以降、20**または**前の 20**上部または問題の一覧の下部にあります。  
  
 レポートを選択して、保存されている最大 5 つのレポートを表示することができます、**レポート**ドロップダウン リスト ボックス。 レポートは、生成日時を示すタイムスタンプ順に一覧表示されます。  
  
## <a name="report-format"></a>レポート形式  
 レポート ビューアーには、レポート内の問題が 3 列で表示されます。 それぞれの問題を折りたたむと、説明が非表示になり、重要な情報だけが表示されます。  
  
 最初の列は、**重要度**列。 アイコンは各問題の重要度を示します。移行がブロックされる問題や重要な問題の場合は、赤い円の中に X マークが表示されます。警告および情報を表す場合は、黄色い三角形の中に感嘆符が表示されます。 2 番目の列では、**修正時期**、ときに問題を解決する必要がありますを示します。 どちらのレポートを並べ替えることができます、**重要度**または**修正時期**列。 3 番目の列では、**説明**問題のタイトルが表示されます。  
  
 問題を展開して、追加情報、問題の解決に関する詳細情報のリンク、および問題の詳細を示すリンクを表示できます。 問題の詳細情報を入手できるリンクをクリックすると、問題に関する情報および問題を解決するための指示を含むヘルプ トピックが表示されます。 問題を修正するか、アクション項目を管理する完全な問題をマークをオンにした後、**この問題が解決された**チェック ボックスをオンします。 アップグレードに関する問題の一覧から解決済み懸案事項を削除する場合は、クリックして**更新**します。 同じコンポーネントに対してアップグレード アドバイザー分析ウィザードを実行するかを適用するまで、問題が再び表示されない、**問題の解決**からフィルター処理、**フィルターによって**オプション。  
  
## <a name="report-files"></a>レポート ファイル  
 アップグレード アドバイザー分析ウィザードでは、My Documents にレポートを作成\\[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Upgrade advisor \110\reports ディレクトリおよび分析するサーバーごとにサブディレクトリが作成されます。 レポート ファイルは、特定の名前付け規則に従った XML ファイルです。 アップグレード アドバイザー レポート ビューアーを起動すると、既定のディレクトリにあるレポート ファイルが表示されます。 レポート ファイルをこのフォルダーにコピーする場合、名前付け規則に従う必要があります。名前付け規則に従わないと、レポート ビューアーでレポート ファイルが自動的に表示されません。  
  
 他のユーザーと情報を共有するには、XML レポートを他のユーザーに送信できます。 また、レポートをコンマ区切り形式のファイルにエクスポートすれば、スプレッドシート、テキスト ファイル、電子メール メッセージなどを別のアプリケーションで作成できます。  
  
## <a name="see-also"></a>参照  
 [方法:アップグレード アドバイザー レポートを表示します。](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)   
 [方法:レポートのエクスポート](../../../2014/sql-server/install/how-to-export-reports.md)   
 [方法:レポートのフィルター](../../../2014/sql-server/install/how-to-filter-reports.md)   
 [アップグレードの問題を解決します。](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
