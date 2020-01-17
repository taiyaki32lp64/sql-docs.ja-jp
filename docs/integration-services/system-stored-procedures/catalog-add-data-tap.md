---
title: catalog.add_data_tap | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: a25ebcc7-535e-4619-adf6-4e2b5a62ba37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 513e4874c858d6ce83b65a9a846aa05617229481
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71295572"
---
# <a name="catalogadd_data_tap"></a>catalog.add_data_tap 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  パッケージ データ フロー内のコンポーネントの出力で、実行のインスタンスのデータ タップを追加します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog.add_data_tap [ @execution_id = ] execution_id  
, [ @task_package_path = ] task_package_path  
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id OUTPUT  
```  
  
## <a name="arguments"></a>引数  
 [ @execution_id = ] *execution_id*  
 パッケージを含む実行の実行 ID。 *execution_id* は **bigint** です。  
  
 [ @task_package_path = ] *task_package_path*  
 データ フロー タスクのパッケージ パス。 データ フロー タスクの **PackagePath** プロパティはパスを指定します。 パスの大文字と小文字は区別されます。 パッケージ パスを特定するには、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] でデータ フロー タスクを右クリックし、 **[プロパティ]** をクリックします。 **[プロパティ]** ウィンドウに、 **[PackagePath]** プロパティが表示されます。  
  
 *task_package_path* は **nvarchar (max)** です。  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 データ フロー パスの識別文字列。 パスは、2 つのデータ フロー コンポーネントを連結します。 パスの **IdentificationString** プロパティは文字列を指定します。  
  
 識別文字列を特定するには、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] で 2 つのデータ フロー コンポーネント間のパスを右クリックし、 **[プロパティ]** をクリックします。 **[プロパティ]** ウィンドウに、 **[IdentificationString]** プロパティが表示されます。  
  
 *dataflow_path_id_string* は **nvarchar (4000)** です。  
  
 [ @data_filename = ] *data_filename*  
 タップされたデータを格納するファイルの名前。 データ フロー タスクが Foreach Loop コンテナーまたは For Loop コンテナーの中で実行される場合、ループの反復ごとにタップされたデータが個別のファイルに格納されます。 各ファイルの先頭には、反復に対応する番号が付けられます。  
  
 既定では、ファイルが格納されている、\<*ドライブ*>: \Program Files\Microsoft SQL Server\130\DTS\DataDumps フォルダーです。  
  
 *data_filename* は **nvarchar (4000)** です。  
  
 [ @max_rows = ] *max_rows*  
 データ タップ中にキャプチャされる行の数。 この値が指定されていない場合は、すべての行がキャプチャされます。 *max_rows* は **int** です。  
  
 [ @data_tap_id = ] *data_tap_id*  
 データ タップの ID を返します。 *data_tap_id* は **bigint** です。  
  
## <a name="example"></a>例  
 次の例では、データ フロー タスク `\Package\Data Flow Task` において、データ フロー パス `'Paths[OLE DB Source.OLE DB Source Output]` 上にデータ タップが作成されます。 タップされたデータは、DataDumps フォルダー (\<*ドライブ*>: \Program Files\Microsoft SQL Server\130\DTS\DataDumps) の `output0.txt` ファイルに格納されます。  
  
```sql
Declare @execution_id bigint  
Exec SSISDB.Catalog.create_execution @folder_name='Packages',@project_name='SSISPackages', @package_name='Package.dtsx',@reference_id=Null, @use32bitruntime=False, @execution_id=@execution_id OUTPUT  
  
Exec SSISDB.Catalog.set_execution_parameter_value @execution_id,50, 'LOGGING_LEVEL', 0  
  
Exec SSISDB.Catalog.add_data_tap @execution_id, @task_package_path='\Package\Data Flow Task', @dataflow_path_id_string = 'Paths[OLE DB Source.OLE DB Source Output]', @data_filename = 'output0.txt'  
  
Exec SSISDB.Catalog.start_execution @execution_id  
```  
  
## <a name="remarks"></a>Remarks  
 データ タップを追加するには、実行のインスタンスが作成された状態である必要があります ([catalog.operations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューの **[状態]** 列の値が 1)。 実行を処理すると状態の値が変わります。 [catalog.create_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)を呼び出すことによって、実行を作成できます。  
  
 add_data_tap ストアド プロシージャに関する考慮事項を以下に示します。  
  
-   実行に親パッケージと 1 つまたは複数の子パッケージが含まれる場合、データをタップする対象パッケージごとにデータ タップを追加する必要があります。  
  
-   パッケージに同じ名前の複数のデータ フロー タスクが含まれる場合、task_package_path によって、タップされるコンポーネントの出力を含むデータ フロー タスクが一意に識別されます。  
  
-   データ タップを追加するとき、パッケージの実行前には検証は行われません。  
  
-   サイズが大きいデータ ファイルが生成されないように、データ タップ中にキャプチャされる行数を制限することをお勧めします。 ストアド プロシージャが実行されるコンピューターで、データ ファイル用のストレージ領域が不足した場合、パッケージは実行を停止し、エラー メッセージがログに書き込まれます。  
  
-   add_data_tap ストアド プロシージャの実行は、パッケージのパフォーマンスに影響を与えます。 ストアド プロシージャは、データの問題のトラブルシューティングを行うことだけを目的に実行することをお勧めします。  
  
-   タップされたデータを格納するファイルにアクセスするには、ストアド プロシージャが実行されているコンピューターの管理者である必要があります。 また、データ タップされたパッケージを含む実行を開始したユーザーであることも必要です。  
  
## <a name="return-codes"></a>リターン コード  
 成功した場合は 0 を返します。  
  
 ストアド プロシージャが失敗した場合は、エラーをスローします。  
  
## <a name="result-set"></a>結果セット  
 なし  
  
## <a name="permissions"></a>アクセス許可  
 このストアド プロシージャには、次の権限のいずれかが必要です。  
  
-   実行のインスタンスの MODIFY 権限  
  
-   **ssis_admin** データベース ロールのメンバーシップ  
  
-   **sysadmin** サーバー ロールのメンバーシップ  
  
## <a name="errors-and-warnings"></a>エラーおよび警告  
 ストアド プロシージャが失敗する原因となる条件を以下に示します。  
  
-   ユーザーに MODIFY 権限がない。  
  
-   指定されたパッケージにおいて、指定されたコンポーネントのデータ タップが既に追加済みである。  
  
-   キャプチャする行数に指定した値が無効である。  
  
## <a name="requirements"></a>必要条件  
  
## <a name="external-resources"></a>外部リソース  
 rafael-salas.com のブログ記事「[SSIS 2012: データ タップのピーク](https://go.microsoft.com/fwlink/?LinkId=239983)」  
  
## <a name="see-also"></a>参照  
 [catalog.add_data_tap_by_guid](../../integration-services/system-stored-procedures/catalog-add-data-tap-by-guid.md)  
  
  
