---
title: CREATE SPATIAL INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/10/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SPATIAL INDEX
- CREATE SPATIAL INDEX
- CREATE_SPATIAL_INDEX_TSQL
- SPATIAL_INDEX_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- spatial indexes [SQL Server], creating
- index creation [SQL Server], spatial indexes
- CREATE SPATIAL INDEX statement
- CREATE INDEX statement
ms.assetid: ee6b9116-a7ff-463a-a9f0-b360804d8678
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2bc1c2c7951efceca6d50a30098284f2bc3ef132
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982590"
---
# <a name="create-spatial-index-transact-sql"></a>CREATE SPATIAL INDEX (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の指定したテーブルと列に空間インデックスを作成します。 インデックスはテーブル内にデータがなくても作成できます。 データベース名を修飾して指定することにより、他のデータベース内のテーブルまたはビューにインデックスを作成することもできます。 空間インデックスでは、テーブルにクラスター化主キーが含まれる必要があります。 空間インデックスについては、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```
CREATE SPATIAL INDEX index_name
  ON <object> ( spatial_column_name )  
    {  
       <geometry_tessellation> | <geography_tessellation>  
    }
  [ ON { filegroup_name | "default" } ]  
[;]
  
<object> ::=  
    { database_name.schema_name.table_name | schema_name.table_name | table_name }  
  
<geometry_tessellation> ::=  
{
  <geometry_automatic_grid_tessellation>
| <geometry_manual_grid_tessellation>
}  
  
<geometry_automatic_grid_tessellation> ::=  
{  
    [ USING GEOMETRY_AUTO_GRID ]  
          WITH  (  
        <bounding_box>  
            [ [,] <tessellation_cells_per_object> [ ,...n] ]  
            [ [,] <spatial_index_option> [ ,...n] ]  
                 )  
}  
  
<geometry_manual_grid_tessellation> ::=  
{  
       [ USING GEOMETRY_GRID ]  
         WITH (  
                    <bounding_box>  
                        [ [,]<tessellation_grid> [ ,...n] ]  
                        [ [,]<tessellation_cells_per_object> [ ,...n] ]  
                        [ [,]<spatial_index_option> [ ,...n] ]  
   )  
}
  
<geography_tessellation> ::=  
{  
      <geography_automatic_grid_tessellation> | <geography_manual_grid_tessellation>  
}  
  
<geography_automatic_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_AUTO_GRID ]  
    [ WITH (  
        [ [,] <tessellation_cells_per_object> [ ,...n] ]  
        [ [,] <spatial_index_option> ]  
     ) ]  
}  
  
<geography_manual_grid_tessellation> ::=  
{  
    [ USING GEOGRAPHY_GRID ]  
    [ WITH (  
                [ <tessellation_grid> [ ,...n] ]  
                [ [,] <tessellation_cells_per_object> [ ,...n] ]  
                [ [,] <spatial_index_option> [ ,...n] ]  
                ) ]  
}  
  
<bounding_box> ::=  
{  
      BOUNDING_BOX = ( {  
       xmin, ymin, xmax, ymax
       | <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>, <named_bb_coordinate>
  } )  
}  
  
<named_bb_coordinate> ::= { XMIN = xmin | YMIN = ymin | XMAX = xmax | YMAX=ymax }  
  
<tessellation_grid> ::=  
{
    GRIDS = ( { <grid_level> [ ,...n ] | <grid_size>, <grid_size>, <grid_size>, <grid_size>  }
        )  
}  
<tessellation_cells_per_object> ::=  
{
   CELLS_PER_OBJECT = n
}  
  
<grid_level> ::=  
{  
     LEVEL_1 = <grid_size>
  |  LEVEL_2 = <grid_size>
  |  LEVEL_3 = <grid_size>
  |  LEVEL_4 = <grid_size>
}  
  
<grid_size> ::= { LOW | MEDIUM | HIGH }  
  
<spatial_index_option> ::=  
{  
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
    | DATA_COMPRESSION = { NONE | ROW | PAGE }  
}  
```  
  
## <a name="arguments"></a>引数  

 *index_name*     
 インデックスの名前です。 インデックス名は、テーブル内では一意である必要がありますが、データベース内で一意である必要はありません。 インデックス名は、[識別子](../../relational-databases/databases/database-identifiers.md)の規則に従っている必要があります。  
  
 ON \<object> ( *spatial_column_name* )     
 インデックスを作成するオブジェクト (データベース、スキーマ、またはテーブル) と空間列の名前を指定します。  
  
 *spatial_column_name* には、インデックスの基準となる空間列を指定します。 単一の空間インデックス定義には 1 つの空間列しか指定できませんが、1 つの **geometry** 列または **geography** 列に複数の空間インデックスを作成できます。  
  
 USING      
 空間インデックスのテセレーション スキームを指定します。 このパラメーターは、次の表に示す型固有の値を使用します。  
  
|列のデータ型|テセレーション スキーム|  
|-------------------------|-------------------------|  
|**geometry**|GEOMETRY_GRID|  
|**geometry**|GEOMETRY_AUTO_GRID|  
|**geography**|GEOGRAPHY_GRID|  
|**geography**|GEOGRAPHY_AUTO_GRID|  
  
 空間インデックスは、 **geometry** 型または **geography** 型の列にのみ作成できます。それ以外の場合はエラーが発生します。 指定された型に対して無効なパラメーターが渡された場合、エラーが発生します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がテセレーションを実装するしくみについては、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
 ON *filegroup_name*      
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 指定したファイル グループに、指定したインデックスを作成します。 位置の指定がなく、テーブルがパーティション分割されていない場合、インデックスには、基になるテーブルと同じファイル グループが使用されます。 ファイル グループは既に存在している必要があります。  
  
 ON "default"     
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 既定のファイル グループに、指定したインデックスを作成します。  
  
 このコンテキストでの default という用語はキーワードではありません。 それは、既定ファイル グループの識別子なので、ON "default" または ON [default] のように区切る必要があります。 "default" を指定する場合は、現在のセッションに対して QUOTED_IDENTIFIER オプションが ON である必要があります。 これが既定の設定です。 詳細については、「[SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)」をご覧ください。  
  
 **\<object>::=**     
 インデックスを作成するオブジェクトを、完全修飾または部分的な修飾の形式で指定します。  
  
 *database_name*      
 データベースの名前です。  
  
 *schema_name*     
 テーブルが所属するスキーマの名前を指定します。  
  
 *table_name*      
 インデックスを作成するテーブルの名前を指定します。  
  
[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] では、database_name が現在のデータベースの場合、または database_name が tempdb で、object_name が # で始まる場合に、3 つの要素で構成された名前形式 database_name.[schema_name].object_nam がサポートされます。  
  
### <a name="using-options"></a>USING オプション

 GEOMETRY_GRID      
 使用している **geometry** グリッド テセレーション スキームを指定します。 GEOMETRY_GRID は、**geometry** データ型の列にのみ指定できます。  GEOMETRY_GRID を使用すると、テセレーション スキームを手動で調整できます。  
  
 GEOMETRY_AUTO_GRID      
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 geometry データ型の列にのみ指定できます。 これはこのデータ型の既定値なので、指定しなくてもかまいません。  
  
 GEOGRAPHY_GRID      
 地理グリッド テセレーション スキームを指定します。 GEOGRAPHY_GRID は、**geography** データ型の列にのみ指定できます。  
  
 GEOGRAPHY_AUTO_GRID      
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]  
  
 geography データ型の列にのみ指定できます。  これはこのデータ型の既定値なので、指定しなくてもかまいません。  
  
### <a name="with-options"></a>WITH オプション

BOUNDING_BOX      
境界ボックスの 4 つの座標を定義する 4 つの数値の組を指定します。x-min と y-min は左下隅の座標で、x-max と y-max は右上隅の座標です。  
  
 *xmin*      
 境界ボックスの左下隅の x 座標を指定します。  
  
 *ymin*      
 境界ボックスの左下隅の y 座標を指定します。  
  
 *xmax*     
 境界ボックスの右上隅の x 座標を指定します。  
  
 *ymax*     
 境界ボックスの右上隅の y 座標を指定します。  
  
 XMIN = *xmin*     
 境界ボックスの左下隅の x 座標のプロパティ名と値を指定します。  
  
 YMIN =*ymin*      
 境界ボックスの左下隅の y 座標のプロパティ名と値を指定します。  
  
 XMAX =*xmax*      
 境界ボックスの右上隅の x 座標のプロパティ名と値を指定します。  
  
 YMAX =*ymax*     
 境界ボックスの右上隅の y 座標のプロパティ名と値を指定します。  
  
 > [!NOTE]
 > 境界ボックスの座標は、USING GEOMETRY_GRID 句内でのみ適用されます。  
 >
 > *xmax* は *xmin* よりも大きく、*ymax* は *ymin* よりも大きい必要があります。 *xmax* > *xmin* かつ *ymax* > *ymin* であることを前提に、任意の有効な [float](../../t-sql/data-types/float-and-real-transact-sql.md) 値表現を指定できます。 それ以外の場合は、該当するエラーが発生します。  
 >
 > 既定値はありません。  
 >
 > 境界ボックスのプロパティ名では、データベースの照合順序に関係なく大文字と小文字が区別されません。  
  
 プロパティ名を指定するには、それぞれ一度だけ指定する必要があります。 これらは任意の順序で指定できます。 たとえば、次の 2 つの句は同等です。  
  
- BOUNDING_BOX =( XMIN =*xmin*, YMIN =*ymin*, XMAX =*xmax*, YMAX =*ymax* )  
  
- BOUNDING_BOX =( XMIN =*xmin*, XMAX =*xmax*, YMIN =*ymin*, YMAX =*ymax*)  
  
GRIDS      
テセレーション スキームの各レベルにおけるグリッド密度を定義します。 GEOMETRY_AUTO_GRID と GEOGRAPHY_AUTO_GRID を選択すると、このオプションは無効になります。  
  
 テセレーションについて詳しくは、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
 GRIDS のパラメーターは次のとおりです。  
  
 LEVEL_1     
 第 1 レベル (最上位) のグリッドを指定します。  
  
 LEVEL_2    
 第 2 レベルのグリッドを指定します。  
  
 LEVEL_3    
 第 3 レベルのグリッドを指定します。  
  
 LEVEL_4    
 第 4 レベルのグリッドを指定します。  
  
 LOW    
 そのレベルのグリッドに最も低い密度を指定します。 LOW は、16 個のセル (4 × 4 のグリッド) に相当します。  
  
 **MEDIUM**     
 そのレベルのグリッドに中程度の密度を指定します。 MEDIUM は、64 個のセル (8 × 8 のグリッド) に相当します。  
  
 HIGH     
 そのレベルのグリッドに最も高い密度を指定します。 HIGH は、256 個のセル (16 × 16 のグリッド) に相当します。  
  
> [!NOTE]
> レベル名を使用すると、任意の順序でレベルを指定することも、レベルを省略することもできます。 レベル名を使用する場合は、一貫してレベル名を使ってレベルを指定する必要があります。 レベルを省略した場合は、その密度は既定で MEDIUM に設定されます。  

> [!WARNING]
> 無効な密度を指定すると、エラーが発生します。  
  
CELLS_PER_OBJECT =*n*     
オブジェクトあたりのテセレーション セル数を指定します。テセレーション プロセスでインデックスの単一空間オブジェクトに使用できるセル数です。 *n* には、1 ～ 8192 の整数を指定できます。 無効な数値が渡されるか、指定されたテセレーションの最大セル数より数値が大きい場合は、エラーが発生します。  
  
 CELLS_PER_OBJECT の既定値は次のとおりです。  
  
|USING オプション|オブジェクトあたりの既定のセル数|  
|------------------|------------------------------|  
|GEOMETRY_GRID|**16**|  
|GEOMETRY_AUTO_GRID|**8**|  
|GEOGRAPHY_GRID|**16**|  
|GEOGRAPHY_AUTO_GRID|**12**|  
  
オブジェクトがセルで指定された数よりについて説明している場合は、最上位レベルに *n*、数のセルに応じて使用して完全な最上位レベルのテセレーションを提供する、インデックスを作成します。 その場合、オブジェクトには指定されたセル数よりも多くのセルが割り当てられることがあります。 この場合、最大数は、密度に応じて最上位レベルのグリッドで生成されたセルの数となります。  
  
CELLS_PER_OBJECT 値は、オブジェクトごとのセル数のテセレーション ルールで使用されます。 テセレーション ルールについて詳しくは、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
PAD_INDEX = { ON | **OFF** }     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
インデックスの埋め込みを指定します。 既定値は OFF です。  
  
ON     
*fillfactor* で指定される空き領域のパーセンテージが、インデックスの中間レベルのページに適用されることを示します。  
  
OFF または *fillfactor* の指定なし     
中間レベルのページはほぼ全容量が使用されることを示します。ただし、中間ページにあるキーのセットを考慮して、インデックスに割り当てることのできる、少なくとも 1 行の最大サイズが収まる分の領域は残されます。  
  
PAD_INDEX では FILLFACTOR で指定されるパーセンテージが使用されるので、PAD_INDEX オプションは、FILLFACTOR が指定されている場合にのみ有効です。 FILLFACTOR で指定されるパーセンテージで 1 行分のデータを格納できない場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では内部的に、最小サイズを格納できるパーセンテージにオーバーライドします。 中間インデックス ページの行数は、*fillfactor* の値がどれだけ小さくなっても 2 未満にはなりません。  
  
FILLFACTOR =*fillfactor*     
 **適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 インデックスの作成時または再構築時に、[!INCLUDE[ssDE](../../includes/ssde-md.md)] が各インデックス ページのリーフ レベルをどの程度まで埋めるかを、パーセント値で指定します。 *fillfactor* 値には、1 ～ 100 の整数値を指定してください。 既定値は 0 です。 *fillfactor* が 100 または 0 の場合、[!INCLUDE[ssDE](../../includes/ssde-md.md)] では全容量を使用するリーフ ページでインデックスが作成されます。  
  
> [!NOTE]  
> FILL FACTOR 値 0 と 100 の機能は、まったく同じです。
  
 FILLFACTOR 設定は、インデックスが作成または再構築されるときのみ適用されます。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] では、ページ内で指定されたパーセント分の空き領域は動的に保持されません。 FILL FACTOR 設定を表示するには、[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) カタログ ビューを使用します。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]では、クラスター化インデックスの作成時にデータが再分配されるため、100 未満の FILLFACTOR 値を使ってクラスター化インデックスを作成すると、データ用のストレージ領域のサイズに影響が生じます。  
  
 詳細については、「 [インデックスの FILL FACTOR の指定](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)」を参照してください。  
  
SORT_IN_TEMPDB = { ON | **OFF** }       
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
 tempdb に一時的な並べ替え結果を格納するかどうかを指定します。 既定値は OFF です。  
  
 ON     
 インデックスの構築に使用される並べ替えの中間結果が、tempdb に格納されます。 tempdb がユーザー データベースとは異なるディスク セットにある場合は、インデックスの作成に要する時間が短縮されます。 インデックスの構築中に使用されるディスク領域のサイズは増加します。  
  
 OFF     
 中間の並べ替え結果はインデックスと同じデータベースに格納されます。  
  
 インデックスを作成するためにユーザー データベース内に必要となる領域の他に、tempdb には、並べ替えの中間結果を格納するためにほぼ同じ大きさの追加領域が必要になります。 詳細については、「[インデックスの SORT_IN_TEMPDB オプション](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)」を参照してください。  
  
IGNORE_DUP_KEY =**OFF**     
インデックスの種類が一意になることはないので、空間インデックスには影響しません。 このオプションを ON に設定すると、エラーが発生します。  
  
STATISTICS_NORECOMPUTE = { ON | **OFF**}     
分布統計を再計算するかどうかを指定します。 既定値は OFF です。  
  
 ON    
 古い統計情報は、自動的には再計算されません。  
  
 OFF    
 自動統計更新が有効です。  
  
 自動統計更新を復元するには、STATISTICS_NORECOMPUTE を OFF に設定するか、NORECOMPUTE 句を指定せずに UPDATE STATISTICS を実行します。  
  
> [!IMPORTANT]  
> 分布統計の自動再計算を無効にすると、クエリ オプティマイザーで、テーブルが関与するクエリの最適実行プランが選択されなくなる場合があります。  
  
DROP_EXISTING = { ON | **OFF** }     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
 名前付きの、既存の空間インデックスを削除および再構築することを指定します。 既定値は OFF です。  
  
 ON     
 既存のインデックスは削除され、再構築されます。 指定するインデックス名は、現在存在するインデックスと同じにする必要がありますが、インデックス定義は変更できます。 たとえば、異なる列、並べ替え順、パーティション構成、またはインデックス オプションを指定できます。  
  
 OFF     
 指定するインデックス名が既に存在する場合、エラーが表示されます。  
  
 DROP_EXISTING を使用してインデックスの種類を変更することはできません。  
  
ONLINE =**OFF**      
インデックス操作中に、基となるテーブルとそれに関連する各インデックスに対してクエリやデータ変更を行えないことを指定します。 このバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、空間インデックスに対するオンラインのインデックス構築操作はサポートされていません。 空間インデックスに対してこのオプションを ON に設定すると、エラーが発生します。 ONLINE オプションを省略するか、ONLINE を OFF に設定してください。  
  
 オフラインのインデックス操作で、空間インデックスの作成、再構築、または削除を行う場合は、テーブルで Sch-M (スキーマ修正) ロックが取得されます。 このため、操作中は、すべてのユーザーは基になるテーブルにアクセスできません。  
  
> [!NOTE]  
> オンラインでのインデックス操作は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
ALLOW_ROW_LOCKS = { **ON** | OFF }     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
 行ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON     
 インデックスにアクセスするとき、行ロックが許可されます。 いつ行ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)]によって決定されます。  
  
 OFF     
 行ロックは使用されません。  
  
ALLOW_PAGE_LOCKS = { **ON** | OFF }     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。 
  
 ページ ロックを許可するかどうかを指定します。 既定値は ON です。  
  
 ON    
 ページにアクセスするとき、行ロックが許可されます。 いつページ ロックを使用するかは、[!INCLUDE[ssDE](../../includes/ssde-md.md)] によって決定されます。  
  
 OFF     
 ページ ロックは使用されません。  
  
MAXDOP =*max_degree_of_parallelism*      
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。
  
 インデックス操作中は、`max degree of parallelism` 構成オプションをオーバーライドします。 並列プランの実行で使用されるプロセッサ数を制限するには、MAXDOP を使用します。 最大数は 64 プロセッサです。  
  
> [!IMPORTANT]  
> MAXDOP オブションは構文的にサポートされていますが、CREATE SPATIAL INDEX では、現在は常に単一のプロセッサしか使用されません。  
  
 *max_degree_of_parallelism* は次のように指定できます。  
  
 1     
 並列プラン生成を抑制します。  
  
 \>1    
 現在のシステム ワークロードに基づいて、並列インデックス操作で使用される最大プロセッサ数を指定の数以下に制限します。  
  
 0 (既定値)    
 現在のシステム ワークロードに基づいて、実際の数以下のプロセッサを使用します。  
  
 詳細については、「 [並列インデックス操作の構成](../../relational-databases/indexes/configure-parallel-index-operations.md)」を参照してください。  
  
> [!NOTE]
> 並列インデックス操作は、[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのエディションで使用できるわけではありません。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]の各エディションでサポートされる機能の一覧については、「 [SQL Server 2016 の各エディションがサポートする機能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)」を参照してください。  
  
DATA_COMPRESSION = {NONE | ROW | PAGE}     
**適用対象**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 以降) と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
  
 インデックスで使用されるデータ圧縮のレベルを決定します。  
  
 NONE     
 インデックスでデータの圧縮は使用されません。  
  
 ROW    
 インデックスでデータの行の圧縮が使用されます。  
  
 PAGE    
 インデックスでデータのページの圧縮が使用されます。  
  
## <a name="remarks"></a>Remarks
すべてのオプションは、CREATE SPATIAL INDEX ステートメントごとに 1 回しか指定できません。 オプションを重複して指定すると、エラーが発生します。  
  
空間インデックスは、テーブルの各空間列に 249 個まで作成できます。 特定の空間列に複数の空間インデックスを作成すると、1 つの列の異なるテセレーション パラメーターのインデックスを作成する場合などに便利です。  
  
> [!IMPORTANT]  
> 空間インデックスの作成には、そのほかにもいくつかの制限があります。 詳しくは、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
インデックスの構築では、プロセスの並列処理を利用することはできません。  
  
## <a name="methods-supported-on-spatial-indexes"></a>空間インデックスでサポートされるメソッド
空間インデックスは、特定の条件下で、いくつかのセット指向のジオメトリ メソッドをサポートします。 詳しくは、「[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)」をご覧ください。  
  
## <a name="spatial-indexes-and-partitioning"></a>空間インデックスとパーティション分割
既定では、空間インデックスをパーティション分割されたテーブルに作成すると、インデックスは、テーブルのパーティション構成に従ってパーティション分割されます。 これによって、インデックス データと関連する行が同じパーティションに格納されます。  
  
この場合、ベース テーブルのパーティション構成を変更するには、ベース テーブルのパーティションを分割し直す前に、空間インデックスを削除する必要があります。 この制約を避けるには、空間インデックスの作成時に、"ON filegroup" オプションを指定します。 詳細については、この後の「空間インデックスとファイル グループ」を参照してください。  
  
## <a name="spatial-indexes-and-filegroups"></a>空間インデックスとファイル グループ
既定では、空間インデックスは、インデックスが指定されたテーブルと同じファイル グループにパーティション分割されます。 ファイル グループを指定するとそちらが優先されます。  
  
[ ON { *filegroup_name* | "default" } ]     
空間インデックスにファイル グループを指定すると、インデックスは、テーブルのパーティション構成に関係なく指定したファイル グループに配置されます。  
  
## <a name="catalog-views-for-spatial-indexes"></a>空間インデックスのカタログ ビュー

 次のカタログ ビューは、空間インデックスに固有です。  
  
 [sys.spatial_indexes](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)  
 空間インデックスの主インデックス情報を表します。  
  
 [sys.spatial_index_tessellations](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)  
 各空間インデックスのテセレーション スキームおよびパラメーターに関する情報を表します。  
  
## <a name="additional-remarks-about-creating-indexes"></a>インデックスの作成に関する追加情報

 インデックス作成について詳しくは、「[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)」の「解説」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可
ユーザーは、テーブルまたはビューに対する `ALTER` 権限を持っているか、sysadmin 固定サーバー ロールまたは `db_ddladmin` および `db_owner` 固定データベース ロールのメンバーである必要があります。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-creating-a-spatial-index-on-a-geometry-column"></a>A. 空間インデックスを geometry 列に作成する
次の例では、**geometry** 型の列 `geometry_col` を含む `SpatialTable` というテーブルを作成します。 次に、空間インデックス `SIndx_SpatialTable_geometry_col1` を `geometry_col` に作成します。 この例では、既定のテセレーション スキームを使用し、境界ボックスを指定します。  
  
```sql  
CREATE TABLE SpatialTable(id int primary key, geometry_col geometry);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col1
   ON SpatialTable(geometry_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ) );  
```  
  
### <a name="b-creating-a-spatial-index-on-a-geometry-column"></a>B. 空間インデックスを geometry 列に作成する
次の例では、`SpatialTable` テーブルの `geometry_col` に 2 番目の空間インデックス `SIndx_SpatialTable_geometry_col2` を作成します。 この例では、テセレーション スキームとして `GEOMETRY_GRID` を指定します。 例では、境界ボックス、グリッド レベルごとに異なる密度、およびオブジェクトごとのセル数に 64 も指定しています。 また、インデックスの埋め込みを `ON` に設定します。  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col2  
   ON SpatialTable(geometry_col)  
   USING GEOMETRY_GRID  
   WITH (  
    BOUNDING_BOX = ( xmin=0, ymin=0, xmax=500, ymax=200 ),  
    GRIDS = (LOW, LOW, MEDIUM, HIGH),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="c-creating-a-spatial-index-on-a-geometry-column"></a>C. 空間インデックスを geometry 列に作成する
次の例では、`SpatialTable` テーブルの `geometry_col` に 3 番目の空間インデックス `SIndx_SpatialTable_geometry_col3` を作成します。 この例では、既定のテセレーション スキームを使用します。 例では、境界ボックスを指定し、第 3 レベルと第 4 レベルに異なるセル密度を使用しますが、オブジェクトごとのセル数には既定値を使用します。  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geometry_col3  
   ON SpatialTable(geometry_col)  
   WITH (  
    BOUNDING_BOX = ( 0, 0, 500, 200 ),  
    GRIDS = ( LEVEL_4 = HIGH, LEVEL_3 = MEDIUM ) );  
```  
  
### <a name="d-changing-an-option-that-is-specific-to-spatial-indexes"></a>D. 空間インデックスに固有のオプションを変更する
次の例では、上の例で作成した空間インデックス `SIndx_SpatialTable_geography_col3` に対して、`LEVEL_3` の新しい密度と DROP_EXISTING = ON を指定することで、空間インデックスを再構築します。  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable(geography_col)  
   WITH ( BOUNDING_BOX = ( 0, 0, 500, 200 ),  
        GRIDS = ( LEVEL_3 = LOW ),  
        DROP_EXISTING = ON );  
```  
  
### <a name="e-creating-a-spatial-index-on-a-geography-column"></a>E. 空間インデックスを geography 列に作成する
次の例では、**geography** 型の列 `geography_col` を含む `SpatialTable2` というテーブルを作成します。 次に、空間インデックス `SIndx_SpatialTable_geography_col1` を `geography_col` に作成します。 この例では、GEOGRAPHY_AUTO_GRID テセレーション スキームの既定のパラメーター値を使用します。  
  
```sql  
CREATE TABLE SpatialTable2(id int primary key, object GEOGRAPHY);  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col1
   ON SpatialTable2(object);  
```  
  
> [!NOTE]  
> 地理グリッド インデックスには、境界ボックスは指定できません。
  
### <a name="f-creating-a-spatial-index-on-a-geography-column"></a>F. 空間インデックスを geography 列に作成する
次の例では、`SpatialTable2` テーブルの `geography_col` に 2 番目の空間インデックス `SIndx_SpatialTable_geography_col2` を作成します。 この例では、テセレーション スキームとして `GEOGRAPHY_GRID` を指定します。 レベルごとに異なるグリッド密度、オブジェクトごとのセル数に 64 をそれぞれ指定します。 また、インデックスの埋め込みを `ON` に設定します。  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col2  
   ON SpatialTable2(object)  
   USING GEOGRAPHY_GRID  
   WITH (  
    GRIDS = (MEDIUM, LOW, MEDIUM, HIGH ),  
    CELLS_PER_OBJECT = 64,  
    PAD_INDEX  = ON );  
```  
  
### <a name="g-creating-a-spatial-index-on-a-geography-column"></a>G. 空間インデックスを geography 列に作成する
次の例では、`SIndx_SpatialTable_geography_col3` テーブルの `geography_col` に 3 番目の空間インデックス `SpatialTable2` を作成します。 この例では、既定のテセレーション スキームの GEOGRAPHY_GRID と、既定の CELLS_PER_OBJECT 値 (16) を使用します。  
  
```sql  
CREATE SPATIAL INDEX SIndx_SpatialTable_geography_col3  
   ON SpatialTable2(object)  
   WITH ( GRIDS = ( LEVEL_3 = HIGH, LEVEL_2 = HIGH ) );  
```  
  
## <a name="see-also"></a>参照
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)       
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)       
[CREATE PARTITION FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-function-transact-sql.md)       
[CREATE PARTITION SCHEME &#40;Transact-SQL&#41;](../../t-sql/statements/create-partition-scheme-transact-sql.md)       
[CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)       
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)       
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)       
[DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)       
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)       
[EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)       
[sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)       
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)       
[sys.spatial_index_tessellations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-index-tessellations-transact-sql.md)       
[sys.spatial_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-spatial-indexes-transact-sql.md)       
[空間インデックスの概要](../../relational-databases/spatial/spatial-indexes-overview.md)       
