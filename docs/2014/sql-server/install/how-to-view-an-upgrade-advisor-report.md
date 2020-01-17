---
title: 操作方法:アップグレード アドバイザー レポートの表示 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- displaying reports
- viewing reports
- Upgrade Advisor [SQL Server], reports
- SQL Server Upgrade Advisor, reports
- reports [Upgrade Advisor], viewing
ms.assetid: d13b38af-0ac3-4030-83cd-e7d7825dd09f
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0ae231e380530f11d4c97a917927ed62e99fb47
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66094802"
---
# <a name="how-to-view-an-upgrade-advisor-report"></a>操作方法:アップグレード アドバイザーのレポートを表示する
  アップグレード アドバイザーでは、分析対象として選択したコンポーネントごとにレポートが作成されます。 このトピックでは、アップグレード アドバイザーの開始ページからアップグレード アドバイザーのレポートを表示する方法について説明します。  
  
> [!IMPORTANT]  
>  レポート ビューアーは、標準のファイル名に基づいてファイルを読み込みます。 ファイル名が変更されると、そのファイルは読み込まれません。  
  
### <a name="to-view-a-report"></a>レポートを表示するには  
  
1.  クリックして**開始**、 をクリックして**すべてのプログラム**、 をクリックして **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]** 、順にクリックします **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]アップグレード アドバイザー**します。  
  
2.  アップグレード アドバイザーの開始 ページで、**アップグレード アドバイザー レポート ビューアーの起動**します。  
  
3.  コンピューターの既定の場所にあるレポートを選択するには、次の手順を実行します。  
  
    1.  **Server**一覧で、サーバーを選択します。  
  
    2.  **インスタンスまたはコンポーネント**一覧で、コンポーネントまたはコンポーネントとインスタンスの組み合わせを選択します。  
  
     別の場所でレポートを選択するには、次の手順を実行します。  
  
    1.  をクリックして、**レポートを開く**リンク。  
  
    2.  レポートの場所を参照し、XML ファイルをダブルクリックします。  
  
     アップグレード アドバイザーでは、以前に行った分析の履歴として最大 5 件のレポートが保持されます。 これらのレポートを表示する をクリックして、**レポート**ドロップダウン リスト ボックス、および、レポートを選択します。 レポートは、生成日時を示すタイムスタンプ順に一覧表示されます。  
  
     レポートには、検出されたすべての問題に対して次の詳細が含まれます。  
  
    -   **重要度**問題を解決するは重要度を示します。  
  
    -   **修正時期**を示すかどうかは (またはする必要があります) 問題を解決する前に、またはにアップグレードした後[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]する前に、またはアプリケーションやデータの移行後にいつでもまたは。  
  
    -   問題の簡潔な説明。  
  
4.  レポートに含まれている項目が 20 項目を超える場合、レポートの上部または下部にある緑色の次へ進む矢印をクリックし、次の項目セットを表示します。 前の 20 項目を表示するには、緑色の "戻る" ボタンをクリックします。  
  
5.  レポートを並べ替えるには、列見出しをクリックします。  
  
6.  特定の項目の詳細を表示するには、その項目をクリックします。 問題の説明が追加のオプションと共に表示されます。  
  
    -   この問題が検出された場所オブジェクトを表示するには、次のようにクリックします。**表示するには、オブジェクトが影響を受ける**します。  
  
    -   問題のヘルプを表示する をクリックして**この問題と解決方法に関する詳細情報を表示する**します。  
  
    -   もう一度レポートを表示するときに、問題を隠す、問題、解決済みとしてマークする選択**この問題が解決された**します。  
  
> [!NOTE]  
>  レポートには、検出不可能な問題に対する項目が含まれる場合があります。 これらは、検出できない問題か、または誤って検出された結果が大量に生成される問題です。 をクリックして、**この問題と解決方法に関する詳細情報を表示する**コンポーネントの検出できない問題の一覧を表示するリンク。  
  
## <a name="see-also"></a>参照  
 [方法:レポートのエクスポート](../../../2014/sql-server/install/how-to-export-reports.md)   
 [方法:アップグレード アドバイザー分析ウィザードを実行します。](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [アップグレードの問題を解決します。](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [アップグレード アドバイザーの操作方法に関するトピック](../../../2014/sql-server/install/upgrade-advisor-how-to-topics.md)   
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
