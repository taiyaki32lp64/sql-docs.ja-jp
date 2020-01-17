---
title: 追加、変更、またはレポート パラメーター (レポート ビルダーおよび SSRS) の使用可能な値の削除 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportparameters.availablevalues.f1
- "10455"
- "10071"
ms.assetid: 0e03264c-523f-4c59-b71b-ceef600f75f6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e9944e437be03dd7cfac3cbe6bad7c5224f3b462
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106675"
---
# <a name="add-change-or-delete-available-values-for-a-report-parameter-report-builder-and-ssrs"></a>レポート パラメーターの値の追加、変更、または削除 (レポート ビルダーおよび SSRS)
  レポート パラメーターを作成した後、ユーザーに対して表示する使用可能な値の一覧を指定できます。 使用可能な値の一覧を使用すると、ユーザーがパラメーターに選択できる値が有効な値のみに制限されます。  
  
 使用可能な値は、レポートの実行時にツール バーのレポート パラメーターの横にあるドロップダウン リストに表示されます。 レポート パラメーターは単一値または複数値を表すことができます。 値が複数ある場合は、一覧の先頭に **[すべて選択]** という項目が用意されるため、ユーザーは 1 回のクリックですべての値を選択またはクリアできます。  
  
 静的な値の一覧か、レポート データセットからの一覧を設定できます。 必要に応じてラベル フィールドを指定して、値の表示名を設定できます。 たとえば、[ `ProductID` ] フィールドに基づくパラメーターの場合、パラメーター ラベルに [ `ProductName` ] フィールドを表示できます。 ユーザーはレポートの実行時に製品名から選択できますが、実際に選択される値は対応する [ `ProductID`] です。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
 レポートをパブリッシュした後、パラメーター プロパティの値をレポート サーバーに設定して、レポート作成ツールのレポートで定義される使用可能な値をオーバーライドできます。 詳細については、「[レポート パラメーター &#40;レポート ビルダーおよびレポート デザイナー&#41;](report-parameters-report-builder-and-report-designer.md)」を参照してください。  
  
### <a name="to-add-or-change-the-available-values-for-a-report-parameter"></a>レポート パラメーターに使用可能な値を追加または変更するには  
  
1.  レポート データ ペインで [パラメーター] ノードを展開します。 パラメーターを右クリックし、 **[パラメーターのプロパティ]** をクリックします。 **[レポート パラメーターのプロパティ]** ダイアログ ボックスが表示されます。  
  
    > [!NOTE]  
    >  レポート データ ペインが表示されていない場合は、 **[表示]** をクリックしてから **[レポート データ]** をクリックします。  
  
2.  **[使用できる値]** をクリックします。 使用可能な値のオプションを選択します。  
  
    -   **[値の指定]** をクリックして値のリストを手動で設定し、必要に応じて値の表示名 (ラベル) を設定します。  
  
         **[追加]** をクリックし、 **[値]** ボックスに値を入力します。必要に応じて、 **[ラベル]** ボックスにラベルを入力します。 ラベルを指定しない場合は、値が使用されます。 値を求める式を記述することもできます。 データ型はパラメーターのデータ型と一致する必要があります。 フィールド名は、パラメーターの式では使用できません。 例については、「[一般的に使用されるフィルター &#40;レポート ビルダーおよび SSRS&#41;](commonly-used-filters-report-builder-and-ssrs.md)」を参照してください。  
  
         設定するすべての値に対して、この手順を繰り返します。 この一覧に表示されるアイテムの順序によって、ユーザーに表示されるドロップダウン リストのアイテムの順序が決まります。 一覧のアイテムの順序を変更するには、 **[値]** または **[ラベル]** ボックスをクリックしてアイテムを選択し、上矢印および下矢印ボタンを使用して一覧内のアイテムを上下に移動します。  
  
    -   **[クエリから値を取得]** をクリックして、このパラメーターの値と必要に応じて表示名を取得する既存のデータセットの名前を設定します。  
  
        > [!IMPORTANT]  
        >  同じデータセットに、レポート パラメーターに対応するクエリ パラメーターが含まれている場合は、レポートを実行しようとするとエラー メッセージが表示されます。 このエラーを解決するには、別のデータセットを使用して値を取得します。  
  
         **[データセット]** で、データセットの名前を選択します。  
  
         **[値フィールド]** で、パラメーター値を指定するフィールドの名前を選択します。  
  
         **[ラベル フィールド]** には、パラメーターの表示名を指定するフィールドの名前を選択します。 表示名に個別のフィールドがない場合は、 **[値]** フィールドに選択したものと同じフィールドを選択します。  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートをプレビューすると、パラメーターに使用可能な値のドロップダウン リストが表示されます。  
  
### <a name="to-remove-the-available-values-for-a-report-parameter"></a>レポート パラメーターに使用可能な値を削除するには  
  
1.  レポート データ ペインで [パラメーター] ノードを展開します。 パラメーターを右クリックし、 **[パラメーターのプロパティ]** をクリックします。 **[レポート パラメーター]** ダイアログ ボックスが表示されます。  
  
2.  **[使用できる値]** をクリックします。  
  
3.  **[次のオプションから 1 つを選択]** で **[なし]** をクリックします。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
     レポートをプレビューすると、パラメーターに使用可能な値のドロップダウン リストが表示されなくなります。  
  
## <a name="see-also"></a>参照  
 [レポート パラメーターの順序の変更 (レポート ビルダーおよび SSRS)](change-the-order-of-a-report-parameter-report-builder-and-ssrs.md)   
 [レポート パラメーターの追加、変更、または削除 &#40;レポート ビルダーおよび SSRS&#41;](add-change-or-delete-a-report-parameter-report-builder-and-ssrs.md)   
 [カスケード型パラメーターのレポートへの追加 (レポート ビルダーおよび SSRS)](add-cascading-parameters-to-a-report-report-builder-and-ssrs.md)   
 [レポート パラメーターの既定値の追加、変更、または削除 (レポート ビルダーおよび SSRS)](add-change-or-delete-default-values-for-a-report-parameter.md)   
 [Parameters コレクションの参照 &#40;レポート ビルダーおよび SSRS&#41;](built-in-collections-parameters-collection-references-report-builder.md)   
 [チュートリアル: レポートへのパラメーターの追加 &#40;レポート ビルダー&#41;](../tutorial-add-a-parameter-to-your-report-report-builder.md)   
 [式 &#40;レポート ビルダーおよび SSRS&#41;](expressions-report-builder-and-ssrs.md)  
  
  
