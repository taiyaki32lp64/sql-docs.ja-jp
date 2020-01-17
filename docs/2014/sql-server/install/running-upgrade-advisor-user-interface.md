---
title: アップグレード アドバイザー (ユーザー インターフェイス) を実行している |。Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5aecaea9bef359ad24aebbd20dd5e9547497043b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092447"
---
# <a name="running-upgrade-advisor-user-interface"></a>アップグレード アドバイザーの実行 (ユーザー インターフェイス)
  アップグレード アドバイザーを実行すると、アップグレードの計画時にローカルまたはリモートのコンポーネントを分析できます。 アップグレード アドバイザーでは、各コンポーネントとインスタンスは、分析レポートを生成します。  
  
> [!IMPORTANT]  
>  アップグレード アドバイザーは [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] のリモート インスタンスを分析しません。 [!INCLUDE[ssRS](../../includes/ssrs.md)] のインスタンスを分析するには、[!INCLUDE[ssRS](../../includes/ssrs.md)] がインストールされているコンピューターにアップグレード アドバイザーをインストールしておく必要があります。  
>   
>  分析する[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Integration Services, が必要、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)]インストールと[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]同じコンピューターにインストールします。  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>アップグレード アドバイザー分析ウィザードを実行します。  
 アップグレード アドバイザー分析ウィザードの実行には、次の 6 つの手順があります。  
  
1.  アップグレード アドバイザーの開始ページからウィザードを起動します。  
  
2.  分析するサーバーとコンポーネントを特定します。  
  
3.  認証情報を取得します。  
  
4.  コンポーネントの種類に基づいて追加パラメーターを取得します。  
  
5.  選択したコンポーネントを分析します。  
  
6.  アップグレードの問題に関するレポートを生成します。  
  
 アップグレード アドバイザー分析ウィザードの詳細については、次を参照してください。[方法。アップグレード アドバイザー分析ウィザードを実行](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)します。  
  
 各ステップに必要な特定の情報を参照してください。[アップグレード アドバイザーのユーザー インターフェイス リファレンス](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)します。  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>アップグレード アドバイザー レポート ビューアーを実行しています。  
 アップグレード アドバイザー分析ウィザードによって生成されたレポートを表示するのにには、アップグレード アドバイザー レポート ビューアーを使用します。 レポートを読み込んだら、次の条件でレポートのコンポーネントをフィルター選択できます。  
  
-   すべての問題  
  
-   アップグレードに関するすべての問題  
  
-   アップグレード前の問題  
  
-   移行に関するすべての問題  
  
-   解決した問題  
  
-   未解決の問題  
  
 レポート ビューアーを使用するための操作手順については、次のトピックを参照してください。  
  
-   [方法:アップグレード アドバイザー レポートを表示します。](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [方法:レポートのフィルター](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [方法:レポートのエクスポート](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>参照  
 [方法:アップグレード アドバイザー分析ウィザードを実行します。](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [アップグレード アドバイザーのユーザー インターフェイス リファレンス](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [アップグレードの問題を解決します。](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
