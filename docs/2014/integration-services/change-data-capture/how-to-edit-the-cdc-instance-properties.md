---
title: CDC インスタンスのプロパティを編集する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7a6c719a-3735-43b7-b3ab-dfadd325eca2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 96604a09811626a304502dc05ef4f7e9edcd0359
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771230"
---
# <a name="how-to-edit-the-cdc-instance-properties"></a>CDC インスタンスのプロパティを編集する方法
  この手順では、CDC デザイナー コンソールを使用して CDC インスタンスの構成プロパティを編集する方法について説明します。  
  
### <a name="to-edit-the-cdc-instance-configuration-properties"></a>CDC インスタンスの構成プロパティを編集するには  
  
1.  **[スタート]** メニューの **[CDC デザイナー コンソール]** をクリックします。  
  
2.  左側のペインで **[Change Data Capture]** を展開し、プロパティを編集するインスタンスが含まれているサービスを展開します。  
  
3.  プロパティを編集するインスタンスの名前を選択します。  
  
4.  CDC デザイナー コンソールの右側にある [アクション] ペインで **[プロパティ]** をクリックします。  
  
     プロパティを編集するインスタンスを右クリックして **[プロパティ]** をクリックすることもできます。  
  
5.  プロパティ エディターで、次のタブのプロパティを編集します。  
  
    -   **[Oracle]** : プロパティ エディターの **[Oracle]** タブを使用して、新しいインスタンス ウィザードの [CDC データベースの作成] ページで指定した説明を変更し、Oracle ログ マイニング データベースの接続情報を変更します。  
  
         このタブで編集できる内容の詳細については、「 [Edit the Oracle Database Properties](edit-the-oracle-database-properties.md)」を参照してください。  
  
    -   **[テーブル]** : Oracle ソース データベースから選択したテーブルおよび列を変更するには、 **[テーブル]** タブを使用します。  
  
         このタブで編集できる内容の詳細については、「 [Edit Tables](edit-tables.md)」を参照してください。  
  
    -   **[ スクリプト]** : 補足ログを設定する Oracle ソース データベースでスクリプトを実行または再実行するには、 **[スクリプト]** タブを使用します。  
  
         このタブで実行できる内容の詳細については、「 [Review and Generate Supplemental Logging Scripts](review-and-generate-supplemental-logging-scripts.md)」を参照してください。  
  
    -   **[詳細設定]** : **[詳細設定]** タブを使用すると、CDC インスタンスに特殊なプロパティを追加できます。  
  
         このタブで実行できる内容の詳細については、「 [Edit the Advanced Properties](edit-the-advanced-properties.md)」を参照してください。  
  
  
