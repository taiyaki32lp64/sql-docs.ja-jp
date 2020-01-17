---
title: ソリューション エクスプ ローラーのソースの管理 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual SourceSafe
- SQL Server Management Studio [SQL Server], source control services
- source-controlled files [SQL Server]
- source controls [SQL Server Management Studio], services
- version control services [SQL Server]
- file source control services [SQL Server]
- VSS [Visual SourceSafe]
ms.assetid: 6373adb8-3d81-4945-a9fc-1d0d5799d29a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 788ce615f914dcc8a2a49fba7575061fff0df870
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62843114"
---
# <a name="solution-explorer-source-control"></a>ソリューション エクスプローラーのソース管理
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] ソリューション エクスプ ローラーは、別のソース管理システムに統合できます。 ソリューションまたはプロジェクトをソース管理システムに統合すると、プロジェクト内のスクリプトとクエリを対象に、ファイル アクセスとバージョン管理を制御できるようになります。  
  
## <a name="solution-and-project-source-control"></a>ソリューションとプロジェクトのソース管理  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)]  
  
 ソース管理とは、サーバー ソフトウェアの主要部分がファイルのバージョンを格納および追跡し、ファイルへのアクセスを制御するシステムです。 標準的なソース管理システムは、1 つのソース管理プロバイダー、および 2 つ以上のソース管理クライアントで構成されます。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] はソース管理サービスに統合することができます。 そのため、このツールはソース管理プロバイダーに対するクライアントとして使用できます。 環境を離れることなく、個人およびチームのプロジェクトを簡単に管理できます。 ソース管理プロバイダーは、[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] に含まれていません。  
  
#### <a name="to-select-a-source-control-provider"></a>ソース管理プロバイダーを選択するには  
  
1.  ソース管理プロバイダーのクライアント部分をインストールします。  
  
2.  [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で、 **[ツール]** メニューの **[オプション]** をクリックします。  
  
3.  **オプション** ダイアログ ボックスで、展開**ソース管理**、 をクリックし、**プラグインの選択**ページ。  
  
4.  **現在ソース管理プラグイン**ボックスで、ソース管理プラグインを選択します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
|トピック|説明|  
|-----------|-----------------|  
|[ソース管理の基礎](../../2014/database-engine/source-control-basics.md)|ソース管理に関する基本的な用語を定義し、プロジェクトでソース管理を使用する利点について説明します。|  
|[ソース管理へのソリューションとプロジェクトの追加](../../2014/database-engine/add-solutions-and-projects-to-source-control.md)|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境を使用して、ソース管理にソリューションおよびプロジェクトを追加する方法について説明します。|  
|[ソース管理からソリューションやプロジェクトを開く方法](../../2014/database-engine/open-solutions-and-projects-from-source-control.md)|[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] 環境を使用して、ソース管理の対象であるソリューションおよびプロジェクトを開く方法について説明します。|  
|[チェックアウトの管理](../../2014/database-engine/manage-checkouts.md)|ソリューションやファイルをソース管理からチェックアウトする方法について説明します。|  
|[チェックインの管理](../../2014/database-engine/manage-checkins.md)|ソリューションやファイルをソース管理にチェックインする方法について説明します。|  
|[バージョン情報の設定と取得](../../2014/database-engine/set-and-retrieve-version-information.md)|プロジェクトや項目の履歴を取得したり、項目のローカル コピーを取得したり、2 つの項目のバージョンを比較したりする方法について説明します。|  
|||  
  
## <a name="see-also"></a>参照  
 [ソリューション エクスプ ローラー](../ssms/solution/solution-explorer.md)   
 [ソリューション&#40;SQL Server Management Studio&#41;](../ssms/sql-server-management-studio-ssms.md)   
 [プロジェクト&#40;SQL Server Management Studio&#41;](../ssms/solution/projects-sql-server-management-studio.md)   
 [ソリューションとプロジェクトを管理するためのファイル](../ssms/solution/files-that-manage-solutions-and-projects.md)  
  
  
