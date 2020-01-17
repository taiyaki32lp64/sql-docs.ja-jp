---
title: ミラー テーブルおよび CDC キャプチャ インスタンスの生成 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- mirTab
ms.assetid: 260c1617-eecc-4007-a84d-3c5778ce46b6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1ba543153e90059312223b2477e9cebd63fbaf79
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294715"
---
# <a name="generate-mirror-tables-and-cdc-capture-instances"></a>ミラー テーブルおよび CDC キャプチャ インスタンスの生成

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [ミラー テーブルの生成] ページを使用すると、CDC インスタンスに含めたテーブルのミラー テーブルを生成できます。  
  
 **[実行]** をクリックするとミラー テーブルが作成されます。 テーブルごとに作成の進行状況が表示され、各ミラー テーブルの作成が正常に終了したか、エラーが発生したかを通知するメッセージが表示されます。 エラーが発生した場合は、 **[詳細]** をクリックしてエラーについて説明するダイアログ ボックスを表示します。  
  
 テーブルの作成に失敗した場合は、そのまま続行するか、または失敗したテーブルを削除してから続行するかを選択できます。 ウィザードの実行が終了したら、Oracle ソース データベースでテーブルを修正するか、CDC インスタンスでそのテーブルを使用しないようにするかを選択できます。 テーブルを修正する場合は、 [Edit Tables](../../integration-services/change-data-capture/edit-tables.md)を行うときにそのテーブルを追加できます。  
  
 **[次へ]** をクリックして [Finish](../../integration-services/change-data-capture/finish.md) ページを開きます。  
  
## <a name="see-also"></a>参照  
 [SQL Server 変更データベース インスタンスを作成する方法](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)  
  
  
