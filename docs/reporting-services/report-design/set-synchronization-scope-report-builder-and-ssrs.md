---
title: "同期スコープ (レポート ビルダーおよび SSRS) の設定 |Microsoft ドキュメント"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 302cc9fbe2c49f2d28786b6a1addcecdcafd3ee7
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>同期スコープの設定 (レポート ビルダーおよび SSRS)
  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] の改ページ調整されたレポートでは、インジケーターは、指定されたスコープ内のインジケーター値の範囲全体を同期することによってデータ値を示します。   
    
  既定では、このスコープは、インジケーターを含んでいるテーブルやマトリックスなどのインジケーターの親コンテナーです。 インジケーターの同期は、レポートのレイアウトに応じて変更できます。 たとえば、テーブルなどのデータ領域に行グループがある場合は、インジケーターのスコープとしてそのグループを指定できます。 インジケーターの同期は省略することもできます。  
  
 測定単位などのオプションは、式を使用して設定できます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)」を参照してください。  
  
 レポート内のスコープの説明および設定方法については、「[合計、集計、および組み込みコレクションの式のスコープ (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
## <a name="to-change-the-synchronization-scope-of-an-indicator"></a>インジケーターの同期スコープを変更するには  
  
1.  変更するインジケーターを右クリックし、 **[インジケーターのプロパティ]**をクリックします。  
  
2.  左ペインの **[値と状態]** をクリックします。  
  
3.  **[同期スコープ]** の一覧で、適用するスコープをクリックします。  
  
     インジケーターから同期スコープを削除する **[(なし)]** オプションは、常に使用可能です。 他のオプションはレポートのレイアウトに依存します。  
  
     必要に応じて、 **式** (*[fx]*) ボタンをクリックして、スコープを設定する式を編集します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [インジケーター &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  