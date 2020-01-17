---
title: fn_xe_file_target_read_file (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_xe_file_target_read_file_TSQL
- fn_xe_file_target_read_file
- sys.fn_xe_file_target_read_file_TSQL
- sys.fn_xe_file_target_read_file
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], functions
- fn_xe_file_target_read_file function
- sys.fn_xe_file_target_read_file function
ms.assetid: cc0351ae-4882-4b67-b0d8-bd235d20c901
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 126b05adab3a07099f6c9110e18e54910f5b2f25
ms.sourcegitcommit: e37636c275002200cf7b1e7f731cec5709473913
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2019
ms.locfileid: "73982992"
---
# <a name="sysfn_xe_file_target_read_file-transact-sql"></a>sys.fn_xe_file_target_read_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  拡張イベント非同期ファイル ターゲットによって作成されるファイルを読み取ります。 行ごとに、XML 形式の 1 つのイベントが返されます。  
  
> [!WARNING]  
>  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] および [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]、XEL および XEM 形式で生成されたトレース結果を受け入れます。 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 拡張イベントでは、XEL 形式のトレース結果のみがサポートされます。 SQL Server Management Studio を使用して、トレース結果を XEL 形式で読み取ることをお勧めします。    
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sys.fn_xe_file_target_read_file ( path, mdpath, initial_file_name, initial_offset )  
```  
  
## <a name="arguments"></a>引数  
 *path*  
 読み取るファイルのパスです。 *パス*にはワイルドカードを含めることができ、ファイルの名前を含めることができます。 *パス*は**nvarchar (260)** です。 既定値はありません。 Azure SQL Database のコンテキストでは、この値は Azure Storage 内のファイルの HTTP URL です。
  
 *mdpath*  
 *Path*引数で指定されたファイルまたはファイルに対応するメタデータファイルへのパス。 *mdpath*は**nvarchar (260)** です。 既定値はありません。 SQL Server 2016 以降では、このパラメーターに null を指定できます。
  
> [!NOTE]  
>  [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] には*mdpath*パラメーターは必要ありません。 ただし、以前のバージョンの SQL Server で生成されたログファイルの旧バージョンとの互換性のために保持されています。  
  
 *initial_file_name*  
 *パス*から読み取る最初のファイル。 *initial_file_name*は**nvarchar (260)** です。 既定値はありません。 引数として**null**が指定されている場合は、 *path*で見つかったすべてのファイルが読み取られます。  
  
> [!NOTE]  
>  *initial_file_name*と*initial_offset*はペアの引数です。 いずれかの引数に値を指定する場合は、他の引数の値を指定する必要があります。  
  
 *initial_offset*  
 以前に読み取られた最後のオフセットを指定します。そのオフセットまでのすべてのイベントがスキップされます。 イベントの列挙は、指定されたオフセットの後に開始されます。 *initial_offset*は**bigint**です。 引数として**null**を指定すると、ファイル全体が読み込まれます。  
  
## <a name="table-returned"></a>返されるテーブル  
  
|列名|データ型|[説明]|  
|-----------------|---------------|-----------------|  
|module_guid|**uniqueidentifier**|イベントモジュールの GUID。 NULL 値は許可されません。|  
|package_guid|**uniqueidentifier**|イベント パッケージの GUID です。 NULL 値は許可されません。|  
|object_name|**nvarchar (256)**|イベントの名前です。 NULL 値は許可されません。|  
|event_data|**nvarchar(max)**|イベントの内容 (XML 形式)。 NULL 値は許可されません。|  
|file_name|**nvarchar(260)**|イベントが格納されているファイルの名前。 NULL 値は許可されません。|  
|file_offset|**bigint**|イベントを格納しているファイル内のブロックのオフセット。 NULL 値は許可されません。|  
|timestamp_utc|**datetime2**|**適用対象**: [!INCLUDE[ssSQLv14](../../includes/sssqlv14-md.md)] 以降と [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br />イベントの日付と時刻 (UTC タイムゾーン)。 NULL 値は許可されません。|  

  
## <a name="remarks"></a>Remarks  
 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] で**fn_xe_file_target_read_file**を実行して大きな結果セットを読み取ると、エラーが発生する可能性があります。 結果を**ファイル**モード (**Ctrl + Shift + F キー**) に使用して、大きな結果セットをファイルにエクスポートし、代わりに別のツールでファイルを読み取ります。  
  
## <a name="permissions"></a>アクセス許可  
 サーバーに対する VIEW SERVER STATE 権限が必要です。  
  
## <a name="examples"></a>使用例  
  
### <a name="a-retrieving-data-from-file-targets"></a>A. ファイルターゲットからデータを取得しています  
 すべてのファイルからすべての行を取得する例を次に示します。 この例では、ファイル ターゲットとメタファイルが C:\ drive のトレース フォルダーにあります。  
  
```  
SELECT * FROM sys.fn_xe_file_target_read_file('C:\traces\*.xel', 'C:\traces\metafile.xem', null, null);  
```  
  
## <a name="see-also"></a>参照  
 [拡張イベントの動的管理ビュー](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [Extended Events Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)   
 [拡張イベント](../../relational-databases/extended-events/extended-events.md)  
  
  
