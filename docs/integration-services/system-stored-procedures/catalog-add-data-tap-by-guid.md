---
title: catalog.add_data_tap_by_guid | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
ms.assetid: ed9d7fa3-61a1-4e21-ba43-1ead7dfc74eb
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6d31ad18b9a7de5b045a9ed868d20a0f35ab441b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71281381"
---
# <a name="catalogadd_data_tap_by_guid"></a>catalog.add_data_tap_by_guid 

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  パッケージ データ フロー内の特定のデータ フロー パスに、実行のインスタンスのデータ タップを追加します。  
  
## <a name="syntax"></a>構文  
  
```sql  
catalog add_data_tap_by_guid [ @execution_id = ] execution_id  
, [ @dataflow_task_guid = ] dataflow_task_guid   
, [ @dataflow_path_id_string = ] dataflow_path_id_string  
, [ @data_filename = ] data_filename  
, [ @max_rows = ] max_rows  
, [ @data_tap_id = ] data_tap_id  
```  
  
## <a name="arguments"></a>引数  
 [ @execution_id = ] *execution_id*  
 パッケージを含む実行の実行 ID。 *execution_id* は **bigint** です。  
  
 [ @dataflow_task_guid = ] *dataflow_task_guid*  
 タップするデータ フロー パスを含むパッケージ内のデータ タスク フローの ID。 *dataflow_task_guid* は **uniqueidentifier** です。  
  
 [ @dataflow_path_id_string = ] *dataflow_path_id_string*  
 データ フロー パスの識別文字列。 パスは、2 つのデータ フロー コンポーネントを連結します。 パスの **IdentificationString** プロパティは文字列を指定します。  
  
 識別文字列を特定するには、[!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] で 2 つのデータ フロー コンポーネント間のパスを右クリックし、 **[プロパティ]** をクリックします。 **[プロパティ]** ウィンドウに、 **[IdentificationString]** プロパティが表示されます。  
  
 *dataflow_path_id_string* は **nvarchar (4000)** です。  
  
 [ @data_filename = ] *data_filename*  
 タップされたデータを格納するファイルの名前。 データ フロー タスクが Foreach Loop コンテナーまたは For Loop コンテナーの中で実行される場合、ループの反復ごとにタップされたデータが個別のファイルに格納されます。 各ファイルの先頭には、反復に対応する番号が付けられます。 データ タップ ファイルは、" *\<SQL Server のインストール フォルダー>* \130\DTS\\" フォルダーに書き込まれます。 *data_filename* は **nvarchar (4000)** です。  
  
 [ @max_rows = ] max_rows  
 データ タップ中にキャプチャされる行の数。 この値が指定されていない場合は、すべての行がキャプチャされます。 max_rows は **int** です。  
  
 [ @data_tap_id = ] *data_tap_id*  
 データ タップの ID。 *data_tap_id* は **bigint** です。  
  
## <a name="example"></a>例  
 次の例では、データ フロー タスク `{D978A2E4-E05D-4374-9B05-50178A8817E8}` において、データ フロー パス `Paths[SRC DimDCVentor.OLE DB Source Output]` 上にデータ タップが作成されます。 タップされたデータは、DCVendorOutput.csv ファイルに格納されます。  
  
```sql
exec catalog.add_data_tap_by_guid   @execution_id,   
'{D978A2E4-E05D-4374-9B05-50178A8817E8}',   
'Paths[SRC DimDCVentor.OLE DB Source Output]',   
'D:\demos\datafiles\DCVendorOutput.csv'  
```  
  
## <a name="remarks"></a>Remarks  
 データ タップを追加するには、実行のインスタンスが作成された状態である必要があります ([catalog.operations &#40;SSISDB データベース&#41;](../../integration-services/system-views/catalog-operations-ssisdb-database.md) ビューの **[状態]** 列の値が 1)。 実行を処理すると状態の値が変わります。 [catalog.create_execution &#40;SSISDB データベース&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md)を呼び出すことによって、実行を作成できます。  
  
 add_data_tap_by_guid ストアド プロシージャに関する考慮事項を以下に示します。  
  
-   データ タップを追加するとき、パッケージの実行前には検証は行われません。  
  
-   サイズが大きいデータ ファイルが生成されないように、データ タップ中にキャプチャされる行数を制限することをお勧めします。 ストアド プロシージャが実行されるコンピューターで、データ ファイル用のストレージ領域が不足した場合、ストアド プロシージャは実行を停止します。  
  
-   add_data_tap_by_guid ストアド プロシージャの実行は、パッケージのパフォーマンスに影響を与えます。 ストアド プロシージャは、データの問題のトラブルシューティングを行うことだけを目的に実行することをお勧めします。  
  
-   タップされたデータを格納するファイルにアクセスするには、ストアド プロシージャが実行されているコンピューターの管理者権限が必要です。  
  
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
  
## <a name="see-also"></a>参照  
 [catalog.add_data_tap](../../integration-services/system-stored-procedures/catalog-add-data-tap.md)  
  
  
