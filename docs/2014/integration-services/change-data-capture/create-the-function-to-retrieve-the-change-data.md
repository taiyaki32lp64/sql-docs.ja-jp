---
title: 変更データを取得する関数を作成する | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- incremental load [Integration Services],creating function
ms.assetid: 55dd0946-bd67-4490-9971-12dfb5b9de94
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 28878f96b843a8a557e95d6c4ddf10681f481b8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62771438"
---
# <a name="create-the-function-to-retrieve-the-change-data"></a>変更データを取得する関数を作成する
  変更データの増分読み込みを実行する [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの制御フローが完了したので、次の作業では、変更データを取得するテーブル値関数を作成します。 この関数は、最初の増分読み込みの前に一度作成するだけで済みます。  
  
> [!NOTE]  
>  変更データを取得する関数の作成は、変更データの増分読み込みを実行するパッケージを作成するプロセスにおける 2 番目の手順です。 このパッケージを作成するプロセス全体の説明については、「[Change Data Capture (SSIS)](change-data-capture-ssis.md)」 (変更データ キャプチャ (SSIS)) をご覧ください。  
  
## <a name="design-considerations-for-change-data-capture-functions"></a>変更データ キャプチャの関数の設計に関する考慮事項  
 変更データを取得するには、パッケージのデータ フローの変換元コンポーネントで、次のいずれかの変更データ キャプチャのクエリ関数を呼び出します。  
  
-   **cdc.fn_cdc_get_net_changes_<capture_instance>** このクエリでは、更新ごとに返される単一行に、変更された各行の最終的な状態が格納されます。 ほとんどの場合、差分変更のクエリによって返されるデータのみが必要です。 詳細については、「[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)」を参照してください。  
  
-   **cdc.fn_cdc_get_all_changes_<capture_instance>** このクエリでは、キャプチャ間隔中に各行で行われたすべての変更が返されます。 詳細については、「[cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql)」を参照してください。  
  
 その後、関数によって返された結果を変換元コンポーネントが受け取って下流にある変換や変換先に渡し、その変換によって変更データが最終的な変換先に適用されます。  
  
 ただし、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントは、これらの変更データ キャプチャの関数を直接呼び出すことができません。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントには、クエリから返される列に関するメタデータが必要です。 変更データ キャプチャの関数では、その出力テーブルの列は定義されません。 したがって、この関数では、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントに十分なメタデータが返されません。  
  
 代わりに、テーブル値ラッパー関数を使用します。この種の関数では RETURNS 句にその出力テーブルの列が明示的に定義されるためです。 この列の明示的な定義によって、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントに必要なメタデータを得ることができます。 この関数は、変更データを取得するテーブルごとに作成する必要があります。  
  
 変更データ キャプチャのクエリ関数を呼び出すテーブル値ラッパー関数を作成するには、2 つの方法があります。  
  
-   **sys.sp_cdc_generate_wrapper_function** システム ストアド プロシージャを呼び出して、テーブル値関数を自動的に作成できます。  
  
-   このトピックで解説するガイドラインと例を使用して、独自のテーブル値関数を記述できます。  
  
## <a name="calling-a-stored-procedure-to-create-the-table-valued-function"></a>テーブル値関数を作成するストアド プロシージャの呼び出し  
 必要なテーブル値関数を最も短時間で簡単に作成する方法は、 **sys.sp_cdc_generate_wrapper_function** システム ストアド プロシージャを呼び出すことです。 このストアド プロシージャでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 変換元コンポーネントの要件を厳密に満たすラッパー関数を作成するスクリプトが生成されます。  
  
> [!IMPORTANT]  
>  **sys.sp_cdc_generate_wrapper_function** システム ストアド プロシージャによって、直接、ラッパー関数が作成されるわけではありません。 このストアド プロシージャでは、ラッパー関数の CREATE スクリプトが生成されます。 開発者は、増分読み込みパッケージでラッパー関数が呼び出される前に、ストアド プロシージャによって生成された CREATE スクリプトを実行する必要があります。  
  
 このシステム ストアド プロシージャの使用方法を理解するには、プロシージャの実行内容、プロシージャによって生成されるスクリプト、およびスクリプトによって作成されるラッパー関数を理解する必要があります。  
  
### <a name="understanding-and-using-the-stored-procedure"></a>ストアド プロシージャの概要と使用方法  
 **sys.sp_cdc_generate_wrapper_function** システム ストアド プロシージャでは、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージで使用するためのラッパー関数を作成するスクリプトが生成されます。  
  
 次に、ストアド プロシージャの定義に含まれる最初の数行を示します。  
  
 `CREATE PROCEDURE sys.sp_cdc_generate_wrapper_function`  
  
 `(`  
  
 `@capture_instance sysname = null`  
  
 `@closed_high_end_point bit = 1,`  
  
 `@column_list = null,`  
  
 `@update_flag_list = null`  
  
 `)`  
  
 ストアド プロシージャのパラメーターはすべて省略可能です。 どのパラメーターにも値を指定せずにストアド プロシージャを呼び出すと、ストアド プロシージャでは、アクセス権が与えられているすべてのキャプチャ インスタンスに対してラッパー関数が作成されます。  
  
> [!NOTE]  
>  このストアド プロシージャの構文とそのパラメーターの詳細については、「[sys.sp_cdc_generate_wrapper_function (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sys-sp-cdc-generate-wrapper-function-transact-sql)」をご覧ください。  
  
 ストアド プロシージャでは、常に、各キャプチャ インスタンスからすべての変更を返すラッパー関数が生成されます。 キャプチャ インスタンスの作成時に *@supports_net_changes* パラメーターを設定した場合は、該当する各キャプチャ インスタンスから差分変更を返すラッパー関数も生成されます。  
  
 このストアド プロシージャによって返される結果セットには、次の 2 つの列が含まれています。  
  
-   ストアド プロシージャによって生成されたラッパー関数の名前。 このストアド プロシージャでは、キャプチャ インスタンス名から関数名を取得します (関数名は、'fn_all_changes_' の後にキャプチャ インスタンス名が続きます。 差分変更追跡の関数が生成された場合、その関数に使用されるプレフィックスは 'fn_net_changes_' です)。  
  
-   ラッパー関数の CREATE ステートメント。  
  
### <a name="understanding-and-using-the-scripts-created-by-the-stored-procedure"></a>ストアド プロシージャによって作成されるスクリプトの概要と使用方法  
 通常、開発者は、INSERT...EXEC ステートメントを使用して **sys.sp_cdc_generate_wrapper_function** ストアド プロシージャを呼び出し、ストアド プロシージャによって作成されるスクリプトを一時テーブルに保存します。 その後、各スクリプトを個別に選択して実行し、対応するラッパー関数を作成できます。 ただし、次のサンプル コードに示すように、開発者は、一連の SQL コマンドを使用して、すべての CREATE スクリプトを実行することもできます。  
  
```  
create table #wrapper_functions  
      (function_name sysname, create_stmt nvarchar(max))  
insert into #wrapper_functions  
exec sys.sp_cdc_generate_wrapper_function  
  
declare @stmt nvarchar(max)  
declare #hfunctions cursor local fast_forward for   
      select create_stmt from #wrapper_functions  
open #hfunctions  
fetch #hfunctions into @stmt  
while (@@fetch_status <> -1)  
begin  
      exec sp_executesql @stmt  
      fetch #hfunctions into @stmt  
end  
close #hfunctions  
deallocate #hfunctions  
```  
  
### <a name="understanding-and-using-the-functions-created-by-the-stored-procedure"></a>ストアド プロシージャによって作成される関数の概要と使用方法  
 キャプチャした変更データのタイムラインを体系的に進めるために、生成されたラッパー関数では、ある期間の *@end_time* パラメーターがその次の期間の *@start_time* パラメーターになることを想定しています。 この規則に従うと、生成されたラッパー関数では次のタスクを実行できます。  
  
-   内部で使用される LSN 値に日付/時刻値をマップします。  
  
-   データの欠落や重複を防ぎます。  
  
 変更テーブルのすべての行に対するクエリの実行を簡略化するために、生成されたラッパー関数では、次の規則もサポートされています。  
  
-   @start_time パラメーターが NULL の場合、ラッパー関数では、キャプチャ インスタンスの最小 LSN 値がクエリの下限として使用されます。  
  
-   @end_time パラメーターが NULL の場合、ラッパー関数では、キャプチャ インスタンスの最大 LSN 値がクエリの上限として使用されます。  
  
 ほとんどのユーザーは、 **sys.sp_cdc_generate_wrapper_function** システム ストアド プロシージャによって作成されたラッパー関数を、変更することなく使用できます。 ただし、ラッパー関数をカスタマイズするには、CREATE スクリプトを実行する前にカスタマイズする必要があります。  
  
 パッケージでは、ラッパー関数を呼び出すときに、3 つのパラメーターの値を指定する必要があります。 この 3 つのパラメーターは、変更データ キャプチャ関数で使用される 3 つのパラメーターに似ています。 この 3 つのパラメーターは次のとおりです。  
  
-   期間の開始日時の値と終了日時の値。 ラッパー関数では、クエリ範囲のエンドポイントとして日付/時刻値が使用されますが、変更データ キャプチャ関数では、エンドポイントとして 2 つの LSN 値が使用されます。  
  
-   行フィルター。 ラッパー関数でも変更データ キャプチャ関数でも、 *@row_filter_option* パラメーターは同じものが使用されます。 詳細については、「[cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62; (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql)」および「[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; (Transact-SQL)](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)」をご覧ください。  
  
 ラッパー関数から返される結果セットには、次のデータが含まれます。  
  
-   変更データの要求されたすべての列。  
  
-   行に関連付けられている操作を示すために 1 文字または 2 文字のフィールドを使用する、__CDC_OPERATION という名前の列。 このフィールドに有効な値は、'I' (挿入)、'D' (削除)、'UO' (古い値の更新)、'UN' (新しい値の更新) です。  
  
-   操作コードの後に、 *@update_flag_list* パラメーターで指定された順にビット列として表示される更新フラグ (要求時)。 これらの列には、関連する列名に '_uflag' が追加された名前が付けられています。  
  
 パッケージで、すべての変更に対してクエリを実行するラッパー関数を呼び出すと、そのラッパー関数は __CDC_STARTLSN 列と \__CDC_SEQVAL 列も返します。 この 2 つの列はそれぞれ、結果セットの 1 番目の列と 2 番目の列になります。 また、ラッパー関数は、この 2 つの列に基づいて結果セットを並べ替えます。  
  
## <a name="writing-your-own-table-value-function"></a>独自のテーブル値関数の作成  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用すると、変更データ キャプチャのクエリ関数を呼び出す独自のテーブル値ラッパー関数を作成して、そのテーブル値ラッパー関数を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納することもできます。 Transact-SQL 関数の作成方法の詳細については、「[CREATE FUNCTION (Transact-SQL)](/sql/t-sql/statements/create-function-transact-sql)」をご覧ください。  
  
 次の例では、指定した変更間隔の Customer テーブルから変更を取得するテーブル値関数を定義します。 この関数では、変更データ キャプチャの関数を使用して、変更テーブルで内部的に使用されるバイナリ ログ シーケンス番号 (LSN) の値に `datetime` 値をマップします。 また、この関数では、次の特殊な条件も処理されます。  
  
-   開始時刻に NULL 値が渡されると、この関数では、使用可能な最も早い時刻値が使用されます。  
  
-   終了時刻に NULL 値が渡されると、この関数では、使用可能な最も遅い時刻値が使用されます。  
  
-   開始 LSN が最終 LSN と同じ場合、この関数は終了します (これは通常、選択した間隔にレコードが存在しないことを示します)。  
  
### <a name="example-of-a-table-value-function-that-queries-for-change-data"></a>変更データをクエリで取得するテーブル値関数の例  
  
```  
CREATE function CDCSample.uf_Customer (  
     @start_time datetime  
    ,@end_time datetime  
)  
returns @Customer table (  
     CustomerID int  
    ,TerritoryID int  
    ,CustomerType nchar(1)  
    ,rowguid uniqueidentifier  
    ,ModifiedDate datetime  
    ,CDC_OPERATION varchar(1)  
) as  
begin  
    declare @from_lsn binary(10), @to_lsn binary(10)  
  
    if (@start_time is null)  
        select @from_lsn = sys.fn_cdc_get_min_lsn('Customer')  
    else  
        select @from_lsn = sys.fn_cdc_increment_lsn(sys.fn_cdc_map_time_to_lsn('largest less than or equal',@start_time))  
  
    if (@end_time is null)  
        select @to_lsn = sys.fn_cdc_get_max_lsn()  
    else  
        select @to_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal',@end_time)  
  
    if (@from_lsn = sys.fn_cdc_increment_lsn(@to_lsn))  
        return  
  
    -- Query for change data  
    insert into @Customer  
    select   
        CustomerID,      
        TerritoryID,   
        CustomerType,   
        rowguid,   
        ModifiedDate,   
        case __$operation  
                when 1 then 'D'  
                when 2 then 'I'  
                when 4 then 'U'  
                else null  
         end as CDC_OPERATION  
    from   
        cdc.fn_cdc_get_net_changes_Customer(@from_lsn, @to_lsn, 'all')  
  
    return  
end   
go  
  
```  
  
### <a name="retrieving-additional-metadata-with-the-change-data"></a>変更データを含む追加のメタデータの取得  
 前述のユーザーが作成したテーブル値関数では **__$operation** 列のみが使用されていますが、**cdc.fn_cdc_get_net_changes_<capture_instance>** 関数では、各変更行の 4 つのメタデータ列を返します。 これらの値をデータ フローで使用する場合は、テーブル値ラッパー関数から追加の列として値を返すことができます。  
  
|列名|データ型|説明|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|`binary(10)`|変更のコミット トランザクションに関連付けられた LSN。<br /><br /> 同じトランザクションでコミットされたすべての変更は、同じコミット LSN を共有します。 たとえば、ソース テーブルの更新操作によって 2 つの異なる行が変更された場合、変更テーブルには、すべて同じ **__$start_lsn** 値を持った 4 つの行 (古い値を含む 2 行と新しい値を含む 2 行) が格納されます。|  
|**__$seqval**|`binary(10)`|特定のトランザクションに含まれる行の変更を並べ替えるためのシーケンス値です。|  
|**__$operation**|`int`|変更に関連付けられているデータ操作言語 (DML) 操作。 次のいずれかになります。<br /><br /> 1 = 削除<br /><br /> 2 = 挿入<br /><br /> 3 = 更新 (更新操作前の値)<br /><br /> 4 = 更新 (更新操作後の値)|  
|**__$update_mask**|`varbinary(128)`|変更された列を識別する、変更テーブルの列序数に基づくビットマスク。 変更された列を特定する必要がある場合にこの値を調べることができます。|  
|**\< キャプチャ対象のソース テーブルの列 >**|各種|この関数によって返されるその他の列は、ソース テーブルの列のうち、キャプチャ インスタンスの作成時にキャプチャ対象として指定された列です。 キャプチャ対象列リストで列が最初に指定されなかった場合、ソース テーブルのすべての列が返されます。|  
  
 詳細については、「[cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql)」を参照してください。  
  
## <a name="next-step"></a>次の手順  
 変更データをクエリで取得するテーブル値関数を作成したら、次の手順で、パッケージのデータ フローのデザインを開始します。  
  
 **次のトピック:** [変更データを取得および理解する](retrieve-and-understand-the-change-data.md)  
  
  
