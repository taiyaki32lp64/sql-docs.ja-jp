---
title: '[サーバーのプロパティ] ([履歴] ページ) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.history.f1
ms.assetid: be9d8018-a46f-4625-9ae1-138ebe6b38ba
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5ce48c964ec756668aa12566c494d9ae9a1e5372
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099582"
---
# <a name="server-properties-history-page"></a>[サーバーのプロパティ]\([履歴] ページ)
  このページを使用すると、保持されるレポート履歴のコピー数の既定値を設定できます。 既定値には、すべてのレポートのレポート履歴の制限を規定する初期設定が用意されています。 これらの設定は、レポートごとに変えることができます。  
  
 レポート履歴は、スナップショット作成時点のレポートで最新だったレポート データとレイアウトが含まれるレポート スナップショットを集めたものです。 レポート履歴を使用すると、特定の日時の状態でレポートのコピーを保持できます。 ネイティブ モードのレポート サーバーまたは SharePoint 統合モード用に構成されたレポート サーバーで実行される個別のレポートについて、レポート履歴を作成および管理することができます。  
  
 レポート履歴スナップショットは、レポート サーバー データベースに格納されます。 スナップショットを無制限に保持する場合は、データベース サイズが急速に増大したり、ディスク領域が過度に消費されていないかどうかを定期的に確認してください。  
  
 このページを開くには、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動してレポート サーバー インスタンスに接続し、レポート サーバー名を右クリックして **[プロパティ]** をクリックします。 **[履歴]** をクリックすると、このページが開きます。  
  
## <a name="options"></a>および  
 **[レポート履歴に無制限の数のスナップショットを保持する]**  
 すべてのレポート履歴スナップショットを保持します。 このレポート ヒストリのサイズを減らすには、スナップショットを手動で削除する必要があります。  
  
 **[レポート履歴のコピーの数を制限する]**  
 設定された数のレポート履歴スナップショットを保持します。 制限値に達すると、古いコピーはレポート ヒストリから順次削除され、空いた領域に新しいコピーが保存されます。  
  
 これから指定するレポート履歴の制限を超えてから、既存のレポート履歴を制限した場合、既存のレポート履歴が新しい制限値まで削減されます。 最初に、最も古いレポート スナップショットが削除されます。 レポート履歴が空であるか、制限を超えていない場合は、新しいレポート スナップショットが追加されます。 制限に達すると、新しいレポート スナップショットが追加されたときに最も古いスナップショットが削除されます。  
  
## <a name="see-also"></a>関連項目  
 [レポート サーバーのプロパティを設定する (Management Studio)](set-report-server-properties-management-studio.md)   
 [Management Studio でレポート サーバーに接続する](connect-to-a-report-server-in-management-studio.md)   
 [Management Studio のレポート サーバーの F1 ヘルプ](report-server-in-management-studio-f1-help.md)  
  
  
