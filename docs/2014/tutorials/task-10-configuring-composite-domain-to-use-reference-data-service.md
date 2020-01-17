---
title: タスク 10:参照データ サービスを使用する複合ドメインの構成 |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 752eefde-8b87-4f54-878e-9963ccbadc8e
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 525e0286d8d82f501981c9e936caca581886b9b4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65481236"
---
# <a name="task-10-configuring-composite-domain-to-use-reference-data-service"></a>タスク 10:参照データ サービスを使用して複合ドメインを構成する
  このタスクで構成する、 **Address Validation**複合ドメインを使用して、**メリッサ データ - アドレスの確認**サービス。 実行時のクレンジング アクティビティでは、クレンジングのために Address Validation ドメインのドメイン値が DQS からこのサービスに渡されます。 参照してください[参照データにドメイン/複合ドメインをマップ](https://msdn.microsoft.com/library/hh213030.aspx)の詳細。  
  
1.  メイン ページで**DQS クライアント**、] をクリックして**Suppliers (ドメイン管理)** [**最近使用したナレッジ ベース**を起動する、**ドメイン管理**ページ。  
  
2.  選択、 **Address Validation**複合ドメインを**ドメインの一覧**します。  
  
3.  右側のウィンドウに切り替えると、**参照データ**タブ。  
  
     ![[データ] タブを参照](../../2014/tutorials/media/et-configuringcdtouserds-01.jpg "参照データ タブ")  
  
4.  クリックして**参照**ツールバーのボタンをクリックします。  
  
5.  **オンライン参照データ プロバイダーのカタログ**ダイアログ ボックスで、**チェック ボックスをオン**横に**Melissa Data の Address Check**します。  
  
     ![Melissa Data のアドレス確認を選択します。](../../2014/tutorials/media/et-configuringcdtouserds-02.jpg "Melissa Data のアドレス確認を選択します。")  
  
6.  右側のウィンドウでの**スキーマ**セクションで、マップ**Address Line**ドメインを**Address Line (M)** ドロップダウン リストを使用して、スキーマ項目。  
  
     ![RDS スキーマ アイテムをドメインにマップ](../../2014/tutorials/media/et-configuringcdtouserds-03.jpg "RDS スキーマ アイテムをドメインにマップします。")  
  
7.  クリックして**スキーマ エントリの追加 (+)** リストにエントリを作成するには、ツールバーのボタンをクリックします。  
  
     ![スキーマ エントリのツール バー ボタンの追加](../../2014/tutorials/media/et-configuringcdtouserds-04.jpg "スキーマ エントリのツール バー ボタンの追加")  
  
8.  次の図に示すように、ドロップダウン リストを使用して次の DQS ドメインをマップします。  
  
     ![RDS スキーマ アイテムをドメインにマッピング](../../2014/tutorials/media/et-configuringcdtouserds-05.jpg "RDS スキーマ アイテムをドメインにマッピングします。")  
  
9. **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
## <a name="next-step"></a>次の手順  
 [タスク 11:ナレッジ ベースをパブリッシュ](../../2014/tutorials/task-11-publishing-the-knowledge-base.md)  
  
  
