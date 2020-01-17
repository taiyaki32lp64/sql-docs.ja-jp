---
title: データ更新履歴 (PowerPivot for SharePoint) の表示 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- data refresh history [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 4c8d8aa8-794d-4f72-ace3-78d0e688e1a5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3efe11a733408124490ece2e85c9bd40db34f3fb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66070919"
---
# <a name="view-data-refresh-history-powerpivot-for-sharepoint"></a>データ更新履歴の表示 (PowerPivot for SharePoint)
  データ更新の履歴とは、Excel ブックの PowerPivot データに対するすべてのデータ更新操作の記録です。 データ更新操作は、指定したスケジュールで SharePoint ファーム内の Analysis Services サーバー インスタンスで実行されます。 既定では、データ更新の履歴は 1 年間保持されます。 ただし、ファーム管理者は、データ更新記録を保持する期間を決定する、使用状況およびイベントの履歴に対する別の保有ポリシーを指定できます。  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  SharePoint 2013 | SharePoint 2010  
  
 **このトピックの内容:**  
  
 [前提条件](#prereq)  
  
 [個々のブックのデータ更新履歴の表示](#viewhistory)  
  
 [すべてのブックのデータ更新履歴の表示](#viewITOps)  
  
 [履歴情報の使用](#pageelements)  
  
##  <a name="prereq"></a> 前提条件  
 データ更新の履歴を表示するには、投稿権限以上の権限が必要です。  
  
 PowerPivot データが含まれているブックに対して、データ更新を有効にし、スケジュールしておく必要があります。 データ更新をスケジュールしていない場合、履歴情報の代わりにスケジュール定義ページが表示されます。  
  
##  <a name="viewhistory"></a> 個々のブックのデータ更新履歴の表示  
  
1.  SharePoint サイトで、PowerPivot データが格納された Excel ブックが含まれているライブラリを開きます。  
  
     SharePoint ライブラリ内のどのブックに PowerPivot データが含まれているかを、外観で判別することはできません。 必要がありますがあらかじめわかっているブックが更新可能な PowerPivot データが含まれています。  
  
2.  ブックを選択し、右側にある下矢印をクリックします。  
  
3.  **[PowerPivot データ更新の管理]** をクリックします。  
  
 履歴ページが開き、現在の Excel ブック内の PowerPivot データに関するすべての更新操作の完全なレコードが表示されます。  
  
##  <a name="viewITOps"></a> すべてのブックのデータ更新履歴の表示  
 サーバーの全体管理で PowerPivot 管理ダッシュボードを使用すると、ファーム管理者およびサービス アプリケーション管理者は、すべての PowerPivot ブックに関するデータ更新の履歴と状態を一括して表示できます。 詳細については、「 [PowerPivot Management Dashboard and Usage Data](power-pivot-management-dashboard-and-usage-data.md)」をご参照ください。  
  
##  <a name="pageelements"></a> 履歴情報の使用  
 データ更新の履歴ページには、各更新操作に関する詳細な情報が表示されます。 このページの情報を使用すると、更新が行われたかどうかを確認したり、更新が失敗した理由を調べたりすることができます。  
  
|アイテム|説明|  
|----------|-----------------|  
|名前|PowerPivot データが含まれている Excel ブックのファイル名を示します。|  
|現在の状態|値は、 **[スケジュール]** 、 **[更新中]** 、 **[成功]** 、 **[失敗]** のいずれかです。<br /><br /> **[スケジュール]** は、初めてスケジュールを作成するときに表示されます。 データ更新が初めて実行された後は、この状態メッセージは表示されなくなります。<br /><br /> **[更新中]** は、データ更新が進行中であることを示します。 要求が処理キューにあるか、サーバーで現在実行中です。<br /><br /> **[成功]** は、前回のデータ更新操作が完了したことを示しており、更新後のブックは SharePoint ライブラリにチェックインされて戻されます。<br /><br /> **[失敗]** は、前回のデータ更新操作が成功しなかったことを示します。 更新後のデータは保存されませんでした。 ブックには、データ更新が開始される前と同じデータが含まれています。|  
|成功した前回の更新|前回のデータ更新が正常に完了した日付を示します。|  
|スケジュールされている次回の更新|次回のデータ更新の実行がスケジュールされている日付を示します。<br /><br /> **[スケジュールの構成]** リンクから、スケジュール定義ページに移動できます。 ブックに対する投稿権限がある場合、このリンクをクリックして、ブック内の PowerPivot データに対する自動データ更新を制御するスケジュール情報を表示および変更することができます。|  
|Started|履歴の詳細セクション内の **[開始]** は、実際の処理時間を示します。 実際の処理時間は、スケジュールとは異なることもあります。 処理が開始されるのは、サーバー上に使用可能なメモリが十分にあるときです。 サーバーの負荷が高い場合、指定した開始時刻よりも数時間遅れて処理が開始されることもあります。|  
|[完了]|履歴の詳細セクション内の **[完了]** は、データ更新操作がいつ終了したかを示します。 日付と時刻は、ブックがライブラリにチェックインされて戻されたときを示します。<br /><br /> データ更新が失敗すると、1 つ以上のエラー メッセージによって、失敗の原因が説明されます。 各レコードを展開して詳細な状態を表示できます。 各データ ソースは、成功メッセージ、またはデータ更新が完了しなかった理由を説明する失敗メッセージと共に、別々に表示されます。|  
|Time|データ更新が開始されてから完了するまでの累積時間を示します。|  
|状態|更新操作が成功したか失敗したかの履歴レコードを示します。|  
  
## <a name="see-also"></a>参照  
 [使用状況データ収集の構成&#40;PowerPivot for SharePoint](configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [データ更新のスケジュール&#40;PowerPivot for SharePoint&#41;](../schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [PowerPivot のデータ更新](power-pivot-data-refresh.md)  
  
  
