---
title: "複数値パラメーターをレポートに追加 |Microsoft ドキュメント"
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
ms.assetid: 12ad0e77-4c28-4bbb-ab11-473ae89ec9f1
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0411de7999d497b3198e6864d185cb54a4a5e1f5
ms.contentlocale: ja-jp
ms.lasthandoff: 08/09/2017

---
# <a name="add-a-multi-value-parameter-to-a-report"></a>複数の値を持つパラメーターのレポートへの追加
  ユーザーがパラメーター値として複数の値を選択できるパラメーターをレポートに追加できます。  
  
 レポート URL に複数のパラメーター値を含めてレポートに渡すことができます。 複数の値を持つパラメーターを含む URL の例は、「 [URL 内でレポート パラメーターを渡す](../../reporting-services/pass-a-report-parameter-within-a-url.md)」を参照してください。  
  
 複数のパラメーター値をストアド プロシージャに渡す方法については、mssqltips.com の「 [SSRS レポートでの複数選択パラメーターの操作](http://go.microsoft.com/fwlink/?LinkId=321529) 」を参照してください。  
  
## <a name="to-add-a-multi-value-parameter"></a>複数の値を持つパラメーターを追加するには  
  
1.  レポート ビルダーで、複数の値を持つパラメーターを追加するレポートを開きます。  
  
2.  レポート データセットを右クリックし、 **[データセットのプロパティ]**をクリックします。  
  
3.  **[クエリ]** ボックスでクエリ テキストを編集するか、クエリ デザイナーを使用してフィルターを追加することで、データセット クエリに変数を追加します。 詳しくは、「[リレーショナル クエリ デザイナーでのクエリの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)」をご覧ください。  
  
    ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    > *  クエリ テキストには、クエリ変数の DECLARE ステートメントを含めないでください。  
    > *  クエリ変数のテキストには、上の例のように、 **IN** 演算子を含める必要があります。  
    > *  上記のように、必ず変数をかっこで囲んでください。 そうしないと、レポートは表示されず、"スカラー変数を宣言してください" というエラーが表示されます。  
  
    埋め込みデータセットまたは共有データセットのデータセット パラメーターは、クエリ変数に対して自動的に作成されます。 レポート パラメーターは、データセット パラメーターに対して自動的に作成されます。  
  
4.  **レポート データ** ペインで **[パラメーター]** ノードを展開し、データセット パラメーターに対して自動的に生成されたレポート パラメーターを右クリックして、 **[パラメーターのプロパティ]**をクリックします。  
  
5.  **[全般]** タブで、 **[複数の値を許可]** を選択して、パラメーターに複数の値を選択できるようにします。  
  
6.  (省略可能) **[使用できる値]** タブで、ユーザーに対して表示する使用可能な値の一覧を指定します。  
  
     使用可能な値の一覧を使用すると、ユーザーがパラメーターに選択できる値が有効な値のみに制限されます。 値が複数ある場合は、一覧の先頭に **[すべて選択]** という項目が用意されるため、ユーザーは 1 回のクリックですべての値を選択またはクリアできます。 レポート パラメーターで使用できる値をデータセット クエリから取得する場合は、同じレポート パラメーターに関連付けられているクエリ変数を含まないデータセットを選択してください。  
  
     詳細については、次を参照してください[追加、変更、またはレポート パラメーター &#40; の使用可能な値の削除。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  
  
## <a name="to-add-a-multi-value-parameter"></a>複数の値を持つパラメーターを追加するには  
  
1.  レポート ビルダーで、複数の値を持つパラメーターを追加するレポートを開きます。  
  
2.  レポート データセットを右クリックし、 **[データセットのプロパティ]**をクリックします。  
  
3.  **[クエリ]** ボックスでクエリ テキストを編集するか、クエリ デザイナーを使用してフィルターを追加することで、データセット クエリに変数を追加します。 詳しくは、「[リレーショナル クエリ デザイナーでのクエリの作成 &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/build-a-query-in-the-relational-query-designer-report-builder-and-ssrs.md)」をご覧ください。  
  
     ```  
    WHERE  
      Production.ProductInventory.ProductID IN (@ProductID)  
    ```  
  
    > [!IMPORTANT]  
    > *  クエリ テキストには、クエリ変数の DECLARE ステートメントを含めないでください。  
    > *  クエリ変数のテキストには、上の例のように、 **IN** 演算子を含める必要があります。  
    > *  上記のように、必ず変数をかっこで囲んでください。 そうしないと、レポートは表示されず、"スカラー変数を宣言してください" というエラーが表示されます。  
      
    埋め込みデータセットまたは共有データセットのデータセット パラメーターは、クエリ変数に対して自動的に作成されます。 レポート パラメーターは、データセット パラメーターに対して自動的に作成されます。  
  
4.  **レポート データ** ペインで **[パラメーター]** ノードを展開し、データセット パラメーターに対して自動的に生成されたレポート パラメーターを右クリックして、 **[パラメーターのプロパティ]**をクリックします。  
  
5.  **[全般]** タブで、 **[複数の値を許可]** を選択して、パラメーターに複数の値を選択できるようにします。  
  
6.  (省略可能) **[使用できる値]** タブで、ユーザーに対して表示する使用可能な値の一覧を指定します。  
  
     使用可能な値の一覧を使用すると、ユーザーがパラメーターに選択できる値が有効な値のみに制限されます。 値が複数ある場合は、一覧の先頭に **[すべて選択]** という項目が用意されるため、ユーザーは 1 回のクリックですべての値を選択またはクリアできます。 レポート パラメーターで使用できる値をデータセット クエリから取得する場合は、同じレポート パラメーターに関連付けられているクエリ変数を含まないデータセットを選択してください。  
  
     詳細については、次を参照してください[追加、変更、またはレポート パラメーター &#40; の使用可能な値の削除。レポート ビルダーおよび SSRS &#41;](../../reporting-services/report-design/add-change-or-delete-available-values-for-a-report-parameter.md).  
  
## <a name="see-also"></a>参照  
 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [レポート パラメーターの追加、変更、または削除 (レポート ビルダーおよび SSRS)](../../reporting-services/report-design/add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)  
  
  