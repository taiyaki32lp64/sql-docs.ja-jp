---
title: 空間インデックスの作成、変更、および削除 | Microsoft Docs
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- indexes [SQL Server], creating
- spatial indexes [SQL Server], dropping
- spatial indexes [SQL Server], creating
- indexes [SQL Server], dropping
- indexes [SQL Server], modifying
- spatial indexes [SQL Server], modifying
ms.assetid: 00c1b927-8ec5-44cf-87c2-c8de59745735
author: MladjoA
ms.author: mlandzic
manager: craigg
ms.openlocfilehash: 7e5dcd71dec0a2189e9f3b51bb7a68b50b070416
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66014267"
---
# <a name="create-modify-and-drop-spatial-indexes"></a>空間インデックスの作成、変更、および削除
  空間インデックスは、の列で特定の操作をより効率的に実行できる、`geometry`または`geography`データ型 (、*列 spatial*)。 1 つの空間列に対して複数の空間インデックスを指定できます。 たとえば、1 つの列の異なるテセレーション パラメーターのインデックスを作成する場合などに便利です。  
  
 空間インデックスの作成にはいくつかの制限があります。 詳細については、このトピックの「 [空間インデックスに関する制限](#restrictions) 」を参照してください。  
  
> [!NOTE]  
>  空間インデックスとパーティションやファイル グループとの関係については、「 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-spatial-index-transact-sql)」の「解説」をご覧ください。  
  
##  <a name="creating"></a> 空間インデックスの作成、変更、および削除  
  
###  <a name="create"></a> 空間インデックスを作成するには  
 **Transact-SQL を使用して空間インデックスを作成するには**  
 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-spatial-index-transact-sql)  
  
 **Management Studio の [新しいインデックス] ダイアログ ボックスを使用して空間インデックスを作成するには**  
 ##### <a name="to-create-a-spatial-index-in-management-studio"></a>Management Studio で空間インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンスに接続し、そのインスタンスを展開します。  
  
2.  **[データベース]** を展開し、指定されたインデックスを含むテーブルが格納されたデータベースを展開して、 **[テーブル]** を展開します。  
  
3.  インデックスを作成するテーブルを展開します。  
  
4.  **[インデックス]** を右クリックして **[新しいインデックス]** をクリックします。  
  
5.  **[インデックス名]** フィールドにインデックスの名前を入力します。  
  
6.  **[インデックスの種類]** ボックスの一覧の **[空間]** をクリックします。  
  
7.  インデックスを作成する空間列を指定するには、 **[追加]** をクリックします。  
  
8.  **から列を選択** *\<テーブル名 >* 型の列の選択 ダイアログ ボックスで、`geometry`または`geography`対応するチェック ボックスをオンにします。 その他の空間列は編集できなくなります。 別の空間列を選択するには、先に現在選択されている列の選択を解除する必要があります。 完了したら、 **[OK]** をクリックします。  
  
9. **[インデックス キー列]** グリッドで、選択した列を確認します。  
  
10. **[インデックスのプロパティ]** ダイアログ ボックスの **[ページの選択]** ペインで、 **[空間]** をクリックします。  
  
11. **[空間]** ページで、インデックスの空間プロパティに対して使用する値を指定します。  
  
     インデックスを作成するとき、`geometry`型の列を指定する必要がある、 **( *`X-min`* 、 *`Y-min`* )** と **( *`X-max`* 、 *`Y-max`* )** 境界ボックスの座標。 インデックスの場合、`geography`型の列で、境界ボックスのフィールド読み取り専用に指定した後、**地理グリッド**テセレーション スキーム、地理グリッド テセレーション スキームは境界ボックスを使用しないためです。  
  
     また、 **[オブジェクトごとのセル数]** フィールドに既定以外の値を指定したり、テセレーション スキームの任意のレベルのグリッド密度を指定したりすることもできます。 オブジェクトごとのセル数の既定値は、 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] では 16、 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 以降では 8 で、 **のグリッド密度の既定値は** [中] [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]です。  
  
     [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]では、テセレーション スキームに GEOMETRY_AUTO_GRID または GEOGRAPHY_AUTO_GRID を選択することができます。 GEOMETRY_AUTO_GRID または GEOGRAPHY_AUTO_GRID を選択すると、レベル 1、レベル 2、レベル 3、およびレベル 4 のグリッド密度のオプションが無効になります。  
  
     これらのプロパティの詳細については、「 [[インデックスのプロパティ] の F1 ヘルプ](../indexes/index-properties-f1-help.md)」をご覧ください。  
  
12. **[OK]** をクリックします。  
  
> [!NOTE]  
>  同じ空間列または異なる空間列に別の空間インデックスを作成するには、上の手順を繰り返します。  
  
  
 **Management Studio のテーブル デザイナーを使用して空間インデックスを作成するには**  
 ##### <a name="to-create-a-spatial-index-in-table-designer"></a>テーブル デザイナーで空間インデックスを作成するには  
  
1.  オブジェクト エクスプローラーで、空間インデックスを作成するテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
     テーブル デザイナーにテーブルが表示されます。  
  
2.  インデックスを作成する `geometry` 列または `geography` 列を選択します。  
  
3.  **[テーブル デザイナー]** メニューの **[空間インデックス]** をクリックします。  
  
4.  **[空間インデックス]** ダイアログ ボックスの **[追加]** をクリックします。  
  
5.  **[選択された空間インデックス]** ボックスの一覧で新しいインデックスを選択し、右側のグリッドで空間インデックスのプロパティを設定します。 プロパティの詳細については、「[[空間インデックス] ダイアログ ボックス &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/visual-database-tools.md)」をご覧ください。  
  
  
###  <a name="alter"></a> 空間インデックスを変更するには  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)  
  
    > [!IMPORTANT]  
    >  BOUNDING_BOX や GRID など、空間インデックス固有のオプションを変更するには、DROP_EXISTING = ON を指定する CREATE SPATIAL INDEX ステートメントを使用するか、空間インデックスを削除して新しく作成します。 例については、「 [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-spatial-index-transact-sql)」の「解説」をご覧ください。  
  
-   [インデックスの変更](../indexes/modify-an-index.md)  
  
-   [既存のインデックスの別のファイル グループへの移動](../indexes/move-an-existing-index-to-a-different-filegroup.md)  
  
  
###  <a name="drop"></a> 空間インデックスを削除するには  
 **Transact-SQL を使用して空間インデックスを削除するには**  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 **Management Studio を使用してインデックスを削除するには**  
 [インデックスの削除](../indexes/delete-an-index.md)  
  
 **Management Studio のテーブル デザイナーを使用して空間インデックスを削除するには**  
 ##### <a name="to-drop-a-spatial-index-in-table-designer"></a>テーブル デザイナーで空間インデックスを削除するには  
  
1.  オブジェクト エクスプローラーで、削除する空間インデックスが含まれているテーブルを右クリックし、 **[デザイン]** をクリックします。  
  
     テーブル デザイナーにテーブルが表示されます。  
  
2.  **[テーブル デザイナー]** メニューの **[空間インデックス]** をクリックします。  
  
     **[空間インデックス]** ダイアログ ボックスが表示されます。  
  
3.  **[選択された空間インデックス]** 列で削除するインデックスをクリックします。  
  
4.  **[削除]** をクリックします。  
  
  
##  <a name="restrictions"></a> 空間インデックスに関する制限  
 空間インデックスを作成できるのは、`geometry` 型か `geography` 型の列だけです。  
  
### <a name="table-and-view-restrictions"></a>テーブルおよびビューの制限  
 空間インデックスは、主キーがあるテーブルでしか定義できません。 テーブルの主キー列の最大数は 15 です。  
  
 インデックス キー レコードの最大サイズは 895 バイトです。 このサイズを超えるとエラーが発生します。  
  
> [!NOTE]  
>  主キーのメタデータは、テーブルに空間インデックスが定義されていると変更できません。  
  
 インデックス付きビューに対して空間インデックスを指定することはできません。  
  
### <a name="multiple-spatial-index-restrictions"></a>複数の空間インデックスに関する制限  
 空間インデックスは、サポートされているテーブルの任意の空間列に 249 個まで作成できます。 同じ空間列に複数の空間インデックスを作成すると、1 つの列の異なるテセレーション パラメーターのインデックスを作成する場合などに便利です。  
  
 一度に作成できる空間インデックスは 1 つだけです。  
  
### <a name="spatial-indexes-and-process-parallelism"></a>空間インデックスとプロセスの並列処理  
 インデックスの構築では、プロセスの並列処理を使用できます。  
  
### <a name="version-restrictions"></a>バージョンの制限事項  
 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] で導入された空間テセレーションは、 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]にレプリケートできません。 [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] のデータベースとの下位互換性が必要条件である場合は、空間インデックスで [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] または [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 空間テセレーションを使用する必要があります。  
  
  
## <a name="see-also"></a>参照  
 [空間インデックスの概要](spatial-indexes-overview.md)  
  
  
