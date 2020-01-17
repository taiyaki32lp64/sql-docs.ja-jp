---
title: Finance の名前ポリシーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 56b2c852-fd69-4cd2-9b5d-977467b94fd9
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a4484f9ccb76ea31c95a5392570e18df2c4b0ff5
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/11/2019
ms.locfileid: "67792913"
---
# <a name="create-the-finance-name-policy"></a>Finance の名前ポリシーの作成
  ここでは、Finance という名前のデータベースを作成し、すべてのテーブルが文字列 **fintbl** で始まることを必須とする条件を作成します。 さらに、Finance データベース内のテーブルに名前付け基準を適用するためのポリシーとポリシー カテゴリを作成します。  
  
### <a name="to-create-the-finance-database"></a>Finance データベースを作成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でクエリ ウィンドウを開き、次のステートメントを実行します。  
  
    ```  
    CREATE DATABASE Finance ;  
    GO  
    ```  
  
2.  オブジェクト エクスプローラーで、 **[データベース]** をクリックし、F5 キーを押してデータベースの一覧を更新します。  
  
### <a name="to-create-the-finance-tables-condition"></a>Finance のテーブルの条件を作成するには  
  
1.  オブジェクト エクスプローラーで、 **[管理]** 、 **[ポリシー管理]** の順に展開し、 **[条件]** を右クリックして **[新しい条件]** をクリックします。  
  
2.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance のテーブル**」と入力します。  
  
3.  **[ファセット]** ボックスの一覧で **[マルチパート名]** を選択します。  
  
4.  **式**領域で、**フィールド**ボックスで、 **\@名前**; で、**演算子**ボックスで、 **ような**; および、**値**ボックスに「 **'fintbl %'** 文字で始まるすべてのテーブル名を強制的に**fintbl**します。  
  
5.  **[説明]** ページで、「 **Finance のテーブル名は必ず fintbl で始める**」と入力し、 **[OK]** をクリックして条件を作成します。  
  
### <a name="to-create-the-finance-name-policy"></a>Finance の名前ポリシーを作成するには  
  
1.  オブジェクト エクスプローラーで **[ポリシー]** を右クリックし、 **[新しいポリシー]** をクリックします。  
  
2.  **[新しいポリシーの作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance の名前**」と入力します。  
  
3.  **[条件の確認]** ボックスの一覧で、 **[Finance のテーブル]** を選択します。 このボックスは **[マルチパート名]** 領域にあります。  
  
4.  **[対象]** 領域に、このポリシーを適用できるデータベース オブジェクトの一覧が表示されます。 **[すべてのテーブル]** のチェック ボックスをオンにします。  
  
5.  **[すべてのデータベース]** 領域で、 **[すべて]** を展開し、 **[新しい条件]** をクリックします。  
  
6.  **[新しい条件の作成]** ダイアログ ボックスで、 **[名前]** ボックスに「 **Finance データベース**」と入力します。  
  
7.  **式**ボックスで式を指定して、完了 **\@名 = 'Finance'** 、順にクリックします**OK**条件ページを閉じます。  
  
    > [!NOTE]  
    >  Tab キーを押して **[値]** ボックスから移動しないと、 **[OK]** ボタンが有効にならない場合があります。  
  
8.  **[評価モード]** の一覧で、 **[変更時: 回避]** を選択します。 これにより、Finance データベースでデータベース トリガーを作成することでポリシーが適用されるようになります。  
  
9. **[有効]** チェック ボックスをオンにします ( **[要求時]** ポリシーには **[有効]** ボックスが適用されません)。  
  
10. **[サーバーの制限]** ボックスの一覧で **[なし]** を選択します。  
  
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-create-the-finance-policy-category"></a>Finance ポリシー カテゴリを作成するには  
  
1.  オブジェクト エクスプローラーで **[管理]** を展開し、 **[ポリシー管理]** を右クリックして、 **[カテゴリの管理]** をクリックします。  
  
2.  **ポリシー カテゴリの管理**ダイアログ ボックスで、**名前**、型`Finance`、空白のボックスと、クリア テキストで**データベースのサブスクリプション**します。 **[データベースのサブスクリプションの要求]** では、インスタンス内のすべてのデータベースは、このポリシー カテゴリに属するポリシーをサブスクライブします。 このレッスンでは、Finance の名前ポリシーをサブスクライブするのは Finance データベースだけです。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="next-task-in-lesson"></a>このレッスンの次の作業  
 [Finance の名前ポリシーのサブスクライブおよび確認](lesson-2-2-subscribe-to-and-check-the-finance-name-policy.md)  
  
  
