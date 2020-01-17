---
title: 空間インデックスストアドプロシージャの引数とプロパティ |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], stored procedures
ms.assetid: ee26082b-c0ed-40ff-b5ad-f5f6b00f0475
author: stevestein
ms.author: sstein
ms.openlocfilehash: 82b906be4568b15a18c55247532bf35b6cd939a7
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69028904"
---
# <a name="spatial-index-stored-procedures---arguments-and-properties"></a>空間インデックスストアドプロシージャ-引数とプロパティ
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  このトピックでは、空間インデックス ストアド プロシージャの引数とプロパティについて説明します。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
 特定の空間インデックスストアドプロシージャの構文については、次のトピックを参照してください。  
  
-   [sp_help_spatial_geometry_index &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="arguments"></a>引数  
`[ @tabname = ] 'tabname'`空間インデックスが指定されているテーブルの修飾名または修飾され名を指定します。  
  
 引用符は、修飾されたテーブルが指定されている場合にのみ必要です。 データベース名を含む完全修飾名を指定する場合は、データベース名を現在のデータベースの名前にする必要があります。 *tabname*は**nvarchar**(776),、既定値はありません。  
  
`[ @indexname = ] 'indexname'`指定された空間インデックスの名前を指定します。 *indexname*は**sysname**で、既定値はありません。  
  
`[ @verboseoutput = ] 'verboseoutput'`返されるプロパティの名前と値の範囲を指定します。  
  
 0 = コアプロパティ  
  
 \>0 = すべてのプロパティ  
  
 *verboseoutput*は**tinyint**で、既定値はありません。  
  
`[ @query_sample = ] 'query_sample'`は、インデックスの有用性をテストするために使用できる代表的なクエリサンプルです。 代表的なオブジェクトまたはクエリウィンドウを指定できます。 *query_sample*は**geometry**既定値はありません。  
  
`[ @xml_output = ] 'xml_output'`XML フラグメントに結果セットを返す出力パラメーターを指定します。 *xml_output*は**xml**で、既定値はありません。  
  
## <a name="properties"></a>Properties  
 次の表に示すように、  **\@verboseoutput** = 0 を設定してコアプロパティを返します。verboseoutput > 0 にすると、空間インデックスのすべてのプロパティが返されます。  **\@**  
  
 **Base_Table_Rows**  
 ベーステーブル内の行の数。 値は**bigint**です。  
  
 **Bounding_Box_xmin**  
 **Geometry**型の空間インデックスの最小の境界ボックスプロパティです。 **Geography**型の場合、このプロパティ値は NULL です。 値は**float**です。  
  
 **Bounding_Box_ymin**  
 **Geometry**型の空間インデックスの Y の最小境界ボックスプロパティです。 **Geography**型の場合、このプロパティ値は NULL です。 値は**float**です。  
  
 **Bounding_Box_xmax**  
 **Geometry**型の空間インデックスの最大境界ボックスのプロパティ (X 座標)。 **Geography**型の場合、このプロパティ値は NULL です。 値は**float**です。  
  
 **Bounding_Box_ymax**  
 **Geometry**型の空間インデックスの最大境界ボックスのプロパティ。 **Geography**型の場合、このプロパティ値は NULL です。 値は**float**です。  
  
 **Grid_Size_Level_1**  
 空間インデックスのレベル1グリッド密度:  
  
 16 (低)  
  
 MEDIUM の場合は 64。  
  
 HIGH の場合は 256。  
  
 値は**int**です。  
  
 **Grid_Size_Level_2**  
 空間インデックスのレベル2のグリッド密度:  
  
 16 (低)  
  
 MEDIUM の場合は 64。  
  
 HIGH の場合は 256。  
  
 値は**int**です。  
  
 **Grid_Size_Level_3**  
 空間インデックスのレベル3のグリッド密度:  
  
 16 (低)  
  
 MEDIUM の場合は 64。  
  
 HIGH の場合は 256。  
  
 値は**int**です。  
  
 **Grid_Size_Level_4**  
 空間インデックスのレベル 4 のグリッド密度。  
  
 16 (低)  
  
 MEDIUM の場合は 64。  
  
 HIGH の場合は 256。  
  
 値は**int**です。  
  
 **Cells_Per_Object**  
 オブジェクトごとのセル数 (インデックスプロパティ)。 値は**int**です。  
  
 **Total_Primary_Index_Rows**  
 インデックス内の行の数。 値は**bigint**です。  
  
 **Total_Primary_Index_Pages**  
 インデックス内のページ数。 値は**bigint**です。  
  
 **Average_Number_Of_Index_Rows_Per_Base_Row**  
 インデックス行の数/ベーステーブルの行の数。 値は**bigint**です。  
  
 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**  
 代表的なクエリサンプルが、**ジオメトリ**インデックスの境界ボックスとルートセル (レベル0のセル) の外にあるかどうかを示します。 この値は、0 (レベル 0 のセル外) または 1 のいずれかです。 レベル 0 のセル内にある場合、調査対象のインデックスは、クエリ サンプルに適切なインデックスではありません。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_ObjectCells_In_Level0_In_Index**  
 レベル 0 (ルートセル、 **geometry**の境界ボックス外) でテセレーションされるインデックス付きオブジェクトのセルインスタンスの数。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Geometry**インデックスの場合は、インデックスの境界ボックスがデータドメインより小さい場合に発生します。 クエリウィンドウが境界ボックスの外側にあり、インデックスのパフォーマンスを低下させる場合 (たとえば、 **Total_Number_Of_ObjectCells_In_Level0_For_QuerySample**が1の場合)、レベル0のオブジェクトの数が多いと、セカンダリフィルターが必要になることがあります。 クエリウィンドウが境界ボックス内にある場合は、レベル0のオブジェクトの数が多いと、インデックスのパフォーマンスが実際に向上する可能性があります。  
  
 NULL および空のインスタンスは、レベル 0 でカウントされますが、パフォーマンスには影響しません。 レベル0には、ベーステーブルの NULL および空のインスタンスと同じ数のセルが含まれます。 **Geography**インデックスでは、クエリサンプルが1としてカウントされるため、レベル0には、NULL および空のインスタンスと同じ数のセルが含まれます。  
  
 **Total_Number_Of_ObjectCells_In_Level1_In_Index**  
 レベル1の精度でテセレーションされるインデックス付きオブジェクトのセルインスタンスの数。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_ObjectCells_In_Level2_In_Index**  
 レベル2の精度でテセレーションされるインデックス付きオブジェクトのセルインスタンスの数。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_ObjectCells_In_Level3_In_Index**  
 レベル3の精度でテセレーションされるインデックス付きオブジェクトのセルインスタンスの数。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_ObjectCells_In_Level4_In_Index**  
 レベル4の精度でテセレーションされるインデックス付きオブジェクトのセルインスタンスの数。 これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level1_In_Index**  
 テセレーションレベル1のオブジェクトによって完全に覆われ、その結果、オブジェクトの内部にあるセルの数。 (Cell_attributevalue は2です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level2_In_Index**  
 テセレーションレベル2のオブジェクトによって完全に覆われ、その結果、オブジェクトの内部にあるセルの数。 (Cell_attribute 値は2です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level3_In_Index**  
 テセレーションレベル3のオブジェクトによって完全に覆われ、その結果、オブジェクトの内部にあるセルの数。 (Cell_attribute 値は2です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_interior_ObjectCells_In_Level4_In_Index**  
 テセレーションレベル4のオブジェクトによって完全に覆われ、その結果、オブジェクトの内部にあるセルの数。 (Cell_attribute 値は2です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level1_In_Index**  
 テセレーションレベル1のオブジェクトと交差するセルの数。 (Cell_attribute 値は1です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level2_In_Index**  
 テセレーションレベル2のオブジェクトと交差するセルの数。 (Cell_attribute 値は1です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level3_In_Index**  
 テセレーションレベル3のオブジェクトが交差するセルの数。 (Cell_attribute 値は1です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_intersecting_ObjectCells_In_Level4_In_Index**  
 テセレーションレベル4のオブジェクトと交差するセルの数。 (Cell_attribute 値は1です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_For_QuerySample**  
 クエリサンプルが境界ボックスの外側のルートセル0にあり、それにタッチするかどうかを示します。 これは、コアプロパティです。 値は**bigint**です。  
  
> [!NOTE]  
>  この情報は、境界ボックスが非常に失われている可能性のあるオブジェクトがあるかどうかを判断する場合にのみ役立ちます。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level0_In_Index**  
 境界ボックスに接しているレベル0のオブジェクトの数。 (Cell_attribute 値は0です)。値は**bigint**です。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level1_In_Index**  
 テセレーションレベル1のグリッドセルの境界に接するオブジェクトセルの数。 (Cell_attribute 値は0です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level2_In_Index**  
 テセレーションレベル2のグリッドセルの境界に接するオブジェクトセルの数。 (Cell_attribute 値は0です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level3_In_Index**  
 テセレーションレベル3のグリッドセルの境界に接するオブジェクトセルの数。 (Cell_attribute 値は0です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Total_Number_Of_Border_ObjectCells_In_Level4_In_Index**  
 テセレーション レベル 4 のグリッド セルの境界に接するオブジェクト セルの数 (Cell_attribute 値は0です)。これは、コアプロパティです。 値は**bigint**です。  
  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 オブジェクトによってカバーされるリーフセルを含むグリッドの合計領域 (リーフセルの合計) の割合。  
  
 たとえば、オブジェクトは、合計で100のリーフセルに相当する領域をカバーする4つの異なるグリッドレベルで、10個のセルにテセレーションされます。 オブジェクトによって完全に覆われた3つの内部セルがあるとします。 3つの内部セルによってカバーされる領域は、42のリーフセルに相当します。 このため、対象領域の割合は 42% です。 これは、インデックス内のオブジェクトがどの程度細分化されているかについての適切な尺度です。  
  
 値は**float**です。  
  
 **Intersecting_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**と同じですが、これらが部分的に覆われたセルである点が異なります。 値は**float**です。  
  
 **Border_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**  
 **Interior_To_Total_Cells_Normalized_To_Leaf_Grid_Percentage**と同じですが、これらが境界セルである点が異なります。 値は**float**です。  
  
 **Average_Cells_Per_Object_Normalized_To_Leaf_Grid**  
 リーフ グリッドに正規化されたオブジェクトごとの平均セル数。 これにより、オブジェクトの空間サイズ、つまりオブジェクトの大きさがわかります。 値は**float**です。  
  
 **Average_Objects_PerLeaf_GridCell**  
 インデックスのスパースの度合い。 リーフセルあたりの平均オブジェクト数。 値は**float**です。  
  
 **Number_Of_SRIDs_Found**  
 インデックスおよび列内の一意な SRID の数。 値は**int**です。  
  
 列には複数の SRID を含めることができ、異なる SRID のオブジェクトは交差しないので、SRID の数はインデックスの選択度を表します。  
  
 **Width_Of_Cell_In_Level1**  
 インデックス作成グリッド内のセルの Width プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Width_Of_Cell_In_Level2**  
 インデックス作成グリッド内のセルの Width プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Width_Of_Cell_In_Level3**  
 インデックス作成グリッド内のセルの Width プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Width_Of_Cell_In_Level4**  
 インデックス作成グリッド内のセルの Width プロパティ。 測定単位はインデックスで指定され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Height_Of_Cell_In_Level1**  
 インデックス作成グリッド内のセルの Height プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Height_Of_Cell_In_Level2**  
 インデックス作成グリッド内のセルの Height プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Height_Of_Cell_In_Level3**  
 インデックス作成グリッド内のセルの Height プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Height_Of_Cell_In_Level4**  
 インデックス作成グリッド内のセルの Height プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Area_Of_Cell_In_Level1**  
 インデックス作成グリッド内のセルの区分プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Area_Of_Cell_In_Level2**  
 インデックス作成グリッド内のセルの区分プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Area_Of_Cell_In_Level3**  
 インデックス作成グリッド内のセルの区分プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **Area_Of_Cell_In_Level4**  
 インデックス作成グリッド内のセルの区分プロパティ。 測定単位はインデックスによって提供され、インデックス付きデータの SRID によって異なります。 値は**float**です。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level1**  
 レベル1のセルによる境界ボックスのカバレッジの割合。 値は**float**です。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level2**  
 レベル2のセルによる境界ボックスのカバレッジの割合。 値は**float**です。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level3**  
 レベル3のセルによる境界ボックスのカバレッジの割合。 値は**float**です。  
  
 **CellArea_To_BoundingBoxArea_Percentage_In_Level4**  
 レベル 4 のセルによる境界ボックスの使用割合。 値は**float**です。  
  
 **Number_Of_Rows_Selected_By_Primary_Filter**  
 プライマリ フィルターによって選択された行数。 これは、コアプロパティです。 値は**bigint です。**  
  
 **Number_Of_Rows_Selected_By_Internal_Filter**  
 内部フィルターによって選択された行数。 これらの行に対しては、セカンダリフィルターは呼び出されません。 これは、コアプロパティです。 値は**bigint です。**  
  
 返される数値は、 **Stintersects**部分にのみ適用されます。  
  
 **Number_Of_Times_Secondary_Filter_Is_Called**  
 セカンダリ フィルターの呼び出し回数。 これは、コアプロパティです。 値は**bigint です。**  
  
 **Percentage_Of_Rows_NotSelected_By_Primary_Filter**  
 ベース テーブル内に N 行あり、P 行がプライマリ フィルターによって選択されたとすると、割合として (N-P)/N を返します。 これは、コアプロパティです。 値は**float です。**  
  
 **Percentage_Of_Primary_Filter_Rows_Selected_By_internal_Filter**  
 P 行がプライマリ フィルターによって選択され、S 行が内部フィルターによって選択されたとすると、割合として S/P を返します。 この割合が大きくなると、インデックスで、パフォーマンス コストが高いセカンダリ フィルターを使用せずに済むようになります。 これは、コアプロパティです。 値は**float です。**  
  
 **Number_Of_Rows_Output**  
 クエリで出力された行数。 これは、コアプロパティです。 値は**bigint です。**  
  
 **Internal_Filter_Efficiency**  
 O が出力された行数である場合は、割合として S/O を返します。 これは、コアプロパティです。 値は**float です。**  
  
 **Primary_Filter_Efficiency**  
 P 行がプライマリフィルターによって選択され、O が出力行数である場合は、割合としてのようになります。 プライマリフィルターの効率が高くなるほど、セカンダリフィルターで処理する必要がある誤検知が減ります。 これは、コアプロパティです。 値は**float です。**  
  
## <a name="permissions"></a>アクセス許可  
 ユーザーは、 **public**ロールのメンバーである必要があります。 サーバーとオブジェクトに対する読み取りアクセス権限が必要です。 これは、すべての空間インデックスストアドプロシージャに適用されます。  
  
## <a name="remarks"></a>コメント  
 NULL 値を含むプロパティは、返されるセットに含まれません。  
  
## <a name="examples"></a>使用例  
 例については、次のトピックを参照してください。  
  
-   [sp_help_spatial_geometry_index &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)  
  
-   [sp_help_spatial_geometry_index_xml &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)  
  
-   [sp_help_spatial_geography_index &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)  
  
-   [sp_help_spatial_geography_index_xml &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-xml-transact-sql.md)  
  
## <a name="requirements"></a>必要条件  
  
## <a name="see-also"></a>関連項目  
 [空間インデックスストアドプロシージャ&#40;transact-sql&#41;](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [XQuery の基礎](../../xquery/xquery-basics.md)   
 [XQuery 言語リファレンス &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)  
  
  
