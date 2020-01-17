---
title: 同期スコープの設定 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 69fa6500439e51705e9dfd3ee838c2f7e1b4eddb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66104995"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>同期スコープの設定 (レポート ビルダーおよび SSRS)
  インジケーターは、指定されたスコープ内のインジケーター値の範囲全体を同期することによってデータ値を示します。 既定では、このスコープは、インジケーターを含んでいるテーブルやマトリックスなどのインジケーターの親コンテナーです。 インジケーターの同期は、レポートのレイアウトに応じて変更できます。 たとえば、テーブルなどのデータ領域に行グループがある場合は、インジケーターのスコープとしてそのグループを指定できます。 インジケーターの同期は省略することもできます。  
  
 測定単位などのオプションは、式を使用して設定できます。 詳細については、「[式 (レポート ビルダーおよび SSRS)](expressions-report-builder-and-ssrs.md)」を参照してください。  
  
 レポート内のスコープの説明および設定方法については、「[合計、集計、および組み込みコレクションの式のスコープ &#40;レポート ビルダーおよび SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)」を参照してください。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-synchronization-scope-of-an-indicator"></a>インジケーターの同期スコープを変更するには  
  
1.  変更し、をクリックするインジケーターを右クリックして**インジケーターのプロパティ**します。  
  
2.  左ペインの **[値と状態]** をクリックします。  
  
3.  **[同期スコープ]** の一覧で、適用するスコープをクリックします。  
  
     インジケーターから同期スコープを削除する **[(なし)]** オプションは、常に使用可能です。 他のオプションはレポートのレイアウトに依存します。  
  
     必要に応じて、 **式** ( *[fx]* ) ボタンをクリックして、スコープを設定する式を編集します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [インジケーター &#40;レポート ビルダーおよび SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
