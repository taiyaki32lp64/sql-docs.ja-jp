---
title: タスク 9:参照データサービスを構成する |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: d0535fce-2bf5-4f6d-b517-ffe6fa13738d
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: e4c756463c43ede8c6dae0cda0a184f0ec7f9956
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154934"
---
# <a name="task-9-configuring-a-reference-data-service"></a>タスク 9:参照データ サービスを構成する
  このタスクでは、Azure Marketplace で参照データサービスを使用するように DQS を構成します。 次のタスクでは、このサービスを使用するように**アドレス検証**ドメインを構成します。 実行時に、クレンジングアクティビティ中に、DQS は、クレンジングのために**アドレス検証**ドメインのドメインの値をサービスに渡します。 詳細については、「[参照データを使用するように DQS を構成する」を](https://msdn.microsoft.com/library/hh213070.aspx)参照してください。  
  
1.  **DQS クライアント**のメインページの **[管理]** ウィンドウで、 **[構成]** をクリックします。  
  
2.  **[参照データ]** タブがアクティブであることを確認します。  
  
3.  プロキシサーバーを使用してインターネットに接続する必要がある場合は、 **[ネットワーク設定]** 領域で、 **[プロキシサーバー]** と **[ポート]** フィールドに適切な値を入力します。  
  
4.  **[DataMarket のアカウント ID]** フィールドに**Azure Marketplace アカウントキー**を入力します。  
  
     ![Azure データマーケットリファレンスデータサービスアカウント](../../2014/tutorials/media/et-configuringareferencedataservice.jpg "Azure データマーケットリファレンスデータサービスアカウント")  
  
5.  アカウント ID を検証するには、テキストボックスの横にある **[検証]** ボタンをクリックします。  
  
6.  メッセージボックスで [ **OK]** をクリックします。  
  
7.  ページの下部にある **[閉じる]** をクリックして、DQS クライアントのメインページに切り替えます。  
  
## <a name="next-task"></a>次の作業  
 [タスク 10:参照データサービスを使用するように複合ドメインを構成する](../../2014/tutorials/task-10-configuring-composite-domain-to-use-reference-data-service.md)  
  
  
