---
title: タスク 16:マスター データ マネージャーを確認する |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 35dd2da7f6cf6598918cd9d109b97f3d314556d1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65484688"
---
# <a name="task-16-verifying-with-master-data-manager"></a>タスク 16:マスター データ マネージャーを確認する
  ここでは、マスター データ マネージャーを使用して、SSIS パッケージによって送信されたバッチ ジョブの状態をチェックし、データが MDS サーバーにアップロードされたことを確認します。  
  
1.  起動**マスター データ マネージャー** ([http://localhost/MDS](http://localhost/MDS))。 既に開いている、クリックして**Microsoft SQL Server マスター データ サービス**に切り替えるの上部にある、**ホーム ページ**。  
  
2.  クリックして**統合管理**します。  
  
3.  という名前のバッチがあることに注意してください**EIMBatch**一覧には、送信します。 クリックして**データのインポート**次の画面が表示されない場合は、メニュー バー。  
  
     ![EIM バッチ](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "EIM バッチ")  
  
4.  をクリックして、ホーム ページに切り替える**SQL Server 2012 マスター データ サービス**上部にあります。  
  
5.  確認します**Suppliers**モデルが選択されている**モデル**と**VERSION_1**が選択されている**バージョン**、 をクリック**エクスプ ローラー**します。  
  
6.  MDS にインポートされたデータの SSIS パッケージが表示されます。 データはクレンジングされており、重複があるない**コード**値 (注。**SupplierID** Excel 列に対応**コード**MDS の Supplier エンティティの属性)。  
  
## <a name="next-step"></a>次の手順  
 [タスク 17:SSIS パッケージによって DQS クレンジング プロジェクトの作成を確認します。](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
