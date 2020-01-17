---
title: レポート データ ペインでのフィールドの追加、編集、更新 (レポート ビルダーおよび SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 2e36f0fe-8100-4513-b169-14d611646f81
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d22a5971d2becebec841c5e343e2361cbe2f26a9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500503"
---
# <a name="add-edit-refresh-fields-in-the-report-data-pane-report-builder-and-ssrs"></a>レポート データ ペインでのフィールドの追加、編集、更新 (レポート ビルダーおよび SSRS)
  データセット フィールドは、外部データ ソースにデータセット クエリを実行するときに返されるデータを表すフィールド名の組み込みのコレクションです。  
  
 埋め込みデータセットのデータセット フィールドには、クエリの作成が完了してクエリ デザイナー ペインを閉じた後に作成されたフィールドと、作成された計算フィールドがあります。  
  
 共有データセットのデータセット フィールドは、レポートに共有データセット定義を追加した際に共有データセット定義から取得されるフィールドです。 レポート サーバー上の共有データセットからのクエリは、レポートの実行時に常に使用されますが、レポート内のデータセット フィールドの一覧は静的です。  
  
 レポート内のフィールドの一覧を更新して共有データセット クエリからのフィールドの現在の一覧に一致させるには、 **[フィールドの更新]** を使用します。 フィールドの一覧を更新しても、レポート内で定義された計算フィールドには影響しません。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-query-field"></a>クエリ フィールドを追加するには  
  
1.  レポート データ ペインでデータセットを右クリックし、 **[クエリ フィールドの追加]** をクリックします。  
  
    > [!NOTE]  
    >  レポート データ ペインを表示できない場合は、 **[表示]** メニューの **[レポート データ]** をクリックします。  
  
2.  **[データセットのプロパティ]** ダイアログ ボックスの **[フィールド]** ページで **[追加]** をクリックし、 **[クエリ フィールド]** をクリックします。 グリッドの下部に、新しい行が追加されます。  
  
3.  **[フィールド名]** ボックスに、フィールドの名前を入力します。  
  
    > [!NOTE]  
    >  名前は、データセット内で一意でなければなりません。  
  
4.  **[フィールド ソース]** ボックスに、データ ソースの既存のフィールドの名前を入力します。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-a-calculated-field"></a>計算フィールドを追加するには  
  
1.  レポート データ ペインでデータセットを右クリックし、 **[計算フィールドの追加]** をクリックします。  
  
2.  **[データセットのプロパティ]** ダイアログ ボックスの **[フィールド]** ページで、 **[追加]** をクリックし、 **[計算フィールド]** をクリックします。 グリッドの下部に、新しい行が追加されます。  
  
3.  **[フィールド名]** ボックスに、フィールドの名前を入力します。  
  
    > [!NOTE]  
    >  名前は、データセット内で一意でなければなりません。  
  
4.  **[フィールド ソース]** ボックスに、フィールドの式を入力します。 式を作成するには、式 ( **[fx]** ) ボタンをクリックします。  
  
    > [!NOTE]  
    >  計算フィールドの式に、レポート アイテムに対する集計または参照を含めることはできません。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-edit-a-query-field-or-a-dataset-field"></a>クエリ フィールドまたはデータセット フィールドを編集するには  
  
1.  レポート データ ペインでフィールドを右クリックし、 **[フィールドのプロパティ]** をクリックします。  
  
2.  **[データセットのプロパティ]** ダイアログ ボックスの **[フィールド]** ページで、既存のフィールドをクリックして行を選択します。  
  
3.  フィールドの名前またはフィールドの値を変更します。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-delete-a-query-field-or-a-calculated-field"></a>クエリ フィールドまたは計算フィールドを削除するには  
  
1.  レポート データ ペインでデータセットを展開して、フィールド コレクションを表示します。  
  
2.  削除するフィールドを右クリックして、 **[削除]** をクリックします。  
  
### <a name="to-refresh-the-field-collection-in-the-report-data-pane-for-a-shared-dataset"></a>共有データセットのレポート データ ペインのフィールド コレクションを更新するには  
  
1.  レポート データ ペインでデータセットを右クリックし、 **[クエリ]** をクリックします。  
  
2.  **[フィールドの更新]** をクリックします。  
  
     レポート サーバーで、共有データセット クエリを実行し、現在のフィールド コレクションを返します。  
  
## <a name="see-also"></a>参照  
 [データセット フィールド コレクション (レポート ビルダーおよび SSRS)](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)   
 [レポート データセット (SSRS)](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [レポート埋め込みデータセットと共有データセット &#40;レポート ビルダーおよび SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Reporting Services クエリ デザイナー](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835)   
 [クエリ デザイン ツール &#40;SSRS&#41;](query-design-tools-ssrs.md)  
  
  
