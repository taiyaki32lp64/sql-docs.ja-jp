---
title: レポートおよび他のアイテムの検索 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6a586659-5c2b-453b-8f40-a3a469277b17
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 76746ade9222257bcea6962c180ea12a01ff8afa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66107646"
---
# <a name="searching-for-reports-and-other-items-report-builder--and-ssrs"></a>レポートおよび他のアイテムの検索 (レポート ビルダーおよび SSRS)
  レポート マネージャーを使用して、名前や説明からレポート サーバーの特定のアイテムを検索できます。 検索できるアイテムは、パブリッシュされているレポート、レポート モデル、フォルダー、共有データ ソース、およびリソースです。 スケジュール、所有者、ロールの割り当て、レポート履歴の特定のスナップショット、またはサブスクリプションは検索できません。 検索は、アイテムが保存されているレポート サーバー データベースに対して実行されます。  
  
> [!NOTE]  
>  ファイル システムの検索を実行しても、レポート サーバーによって管理されているアイテムの検索結果は返されません。  
  
-   レポート マネージャーでアイテムを検索するには、ページの先頭にある **[検索]** テキスト ボックスに検索文字列を入力します。 検索は、フォルダー階層の最上位ノードから開始され、続いて各分岐にわたり実行されます。 特定の分岐へのアクセス権がない場合、その分岐は検索されません。 これには、他のユーザーが所有する [個人用レポート] フォルダー、および通常アクセスできない他のフォルダーが該当します。 検索結果には、表示権限のあるレポートやアイテムのみが表示されます。  
  
-   名前や説明からアイテムを検索するには、検索したいテキストのすべてまたは一部を指定します。 検索文字列の大文字と小文字は区別されません。 検索条件の指定や除外を行う正符号 (+) や負符号 (-) などの検索演算子は使用できません。  
  
-   レポート内の特定のテキストを検索するには、レポートの最上部にあるツール バーを使用します。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="see-also"></a>参照  
 [レポート マネージャーを使用したレポートの検索と表示 (レポート ビルダーおよび SSRS)](finding-and-viewing-reports-in-the-web-portal-report-builder-and-ssrs.md)   
 [個人用レポートの使用 (レポート ビルダーおよび SSRS)](using-my-reports-report-builder-and-ssrs.md)   
 [レポートの検索、表示、管理 (レポート ビルダーおよび SSRS)](finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [レポートを開閉する (レポート マネージャー)](../reports/open-and-close-a-report-report-manager.md)  
  
  
