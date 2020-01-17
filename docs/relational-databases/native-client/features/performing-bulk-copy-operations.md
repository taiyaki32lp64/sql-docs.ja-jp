---
title: 一括コピー操作の実行 |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- bulk copy [SQL Server Native Client]
- data access [SQL Server Native Client], bulk copy operations
- SQL Server Native Client, bulk copy operations
- SQLNCLI, bulk copy operations
ms.assetid: 50d8456b-e6a1-4b25-bc7e-56946ed654a7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 26e518c871f9fc2e3c3be644163295c683e3a970
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73788237"
---
# <a name="performing-bulk-copy-operations"></a>一括コピー操作の実行
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の一括コピー機能により、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルやビューに大量のデータを入出力できます。 SELECT ステートメントを指定してデータを外部に転送することもできます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] と ASCII ファイルなどのオペレーティング システム データ ファイルとの間でデータを移動できます。 データ ファイルには、さまざまな形式を使用できます。一括コピーの形式は、フォーマット ファイルで定義されます。 必要に応じて、データをプログラム変数に読み込んでから、一括コピー関数や一括コピー メソッドを使用して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に転送できます。  
  
 この機能を示すサンプルアプリケーションについては、「 [IRowsetFastLoad &#40;OLE DB&#41;を使用した一括データコピー](../../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)」を参照してください。  
  
 アプリケーションでは、通常、次のいずれかの方法で一括コピーを使用します。  
  
-   テーブル、ビュー、または Transact-SQL ステートメントの結果セットからデータ ファイルに一括コピーします。その際、コピー先のデータ ファイルには、テーブルやビューと同じ形式でデータを格納します。  
  
     これをネイティブモード データ ファイルと呼びます。  
  
-   テーブル、ビュー、または Transact-SQL ステートメントの結果セットからデータ ファイルに一括コピーします。その際、コピー先のデータ ファイルには、テーブルやビューとは異なる形式でデータを格納します。  
  
     この場合、データ ファイルに格納される各列の特性 (データ型、位置、長さ、ターミネータなど) を定義するフォーマット ファイルを別に作成します。 すべての列を文字形式に変換する場合、変換後のファイルをキャラクターモード データ ファイルと呼びます。  
  
-   データ ファイルからテーブルやビューに一括コピーします。  
  
     必要に応じて、フォーマット ファイルを使用してデータ ファイルのレイアウトを決定します。  
  
-   プログラム変数にデータを読み込んでから、毎回 1 行ずつ一括コピーを行う一括コピー関数を使用して、データをテーブルやビューにインポートします。  
  
 一括コピー関数で使用するデータ ファイルを、別の一括コピー プログラムで作成する必要はありません。 他のシステムでも、一括コピー定義に従ってデータ ファイルとフォーマット ファイルを作成できます。その後、これらのファイルを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] の一括コピー プログラムで使用して、データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] にインポートできます。 たとえば、スプレッドシートからタブ区切り形式のファイルにデータをエクスポートし、タブ区切りファイルの形式を示すフォーマット ファイルを作成した後、一括コピー プログラムを使用して、データを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] に簡単にインポートできます。 一括コピーで生成されたデータ ファイルを、他のアプリケーションにインポートすることもできます。 たとえば、一括コピー関数を使用して、スプレッドシートに読み込むことができるタブ区切りファイルとして、テーブルやビューからデータをエクスポートできます。  
  
 一括コピー関数を使用するアプリケーションをコーディングするプログラマは、適切なパフォーマンスで一括コピーを行うための一般的な規則に従う必要があります。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]での一括コピー操作のサポートの詳細については、「 [ &#40;データ SQL Server&#41;の一括インポートと一括エクスポート](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)」を参照してください。  
  
## <a name="limitations-and-restrictions"></a>制限事項と制約事項  
 CLR ユーザー定義型 (UDT) はバイナリ データとしてバインドする必要があります。 フォーマット ファイルで、SQLCHAR がコピー先の UDT 列のデータ型として指定されていたとしても、BCP ユーティリティは、そのデータをバイナリとして扱います。  
  
 一括コピー操作では SET FMTONLY OFF を使用しないでください。 SET FMTONLY OFF を使用すると、一括コピー操作でエラーや予期しない結果が生じることがあります。  
  
## <a name="sql-server-native-client-ole-db-provider"></a>SQL Server Native Client OLE DB プロバイダー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] データベースで一括コピー操作を実行するための2つの方法を実装しています。 1 つ目のメソッドでは、メモリベースの一括コピー操作に [IRowsetFastLoad](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md) インターフェイスを使用します。2 つ目のメソッドでは、ファイルベースの一括コピー操作に [IBCPSession](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md) インターフェイスを使用します。  
  
### <a name="using-memory-based-bulk-copy-operations"></a>メモリ ベースの一括コピー操作の使用  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **IRowsetFastLoad**インターフェイスを実装して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] メモリベースの一括コピー操作のサポートを公開します。 **IRowsetFastLoad** インターフェイスには、[IRowsetFastLoad::Commit](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md) メソッドと [IRowsetFastLoad::InsertRow](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md) メソッドが実装されています。  
  
#### <a name="enabling-a-session-for-irowsetfastload"></a>IRowsetFastLoad のセッションの有効化  
 コンシューマーは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー固有のデータ ソース プロパティである SSPROP_ENABLEFASTLOAD を VARIANT_TRUE に設定することにより、一括コピーを実行する必要があることを [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーに通知します。 コンシューマーはデータ ソースのプロパティ セットを使用して、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー セッションを作成します。 この新しいセッションによって、コンシューマーから **IRowsetFastLoad** インターフェイスにアクセスできるようになります。  
  
> [!NOTE]  
>  データ ソースの初期化に **IDataInitialize** インターフェイスを使用する場合は、*IOpenRowset::OpenRowset* メソッドの **rgPropertySets** パラメーターで SSPROP_IRowsetFastLoad プロパティを設定する必要があります。このプロパティを設定せずに **OpenRowset** メソッドを呼び出すと、E_NOINTERFACE が返されます。  
  
 一括コピー用にセッションを有効にすることで、そのセッションのインターフェイスに対する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのサポートが制限されます。 一括コピーが可能なセッションは、次のインターフェイスのみを公開します。  
  
-   **IDBSchemaRowset**  
  
-   **IGetDataSource**  
  
-   **IOpenRowset**  
  
-   **ISupportErrorInfo**  
  
-   **ITransactionJoin**  
  
 一括コピー可能な行セットの作成を無効にし、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー セッションの処理を標準処理に戻すには、SSPROP_ENABLEFASTLOAD を VARIANT_FALSE にリセットします。  
  
#### <a name="irowsetfastload-rowsets"></a>IRowsetFastLoad 行セット  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの一括コピー行セットは書き込み専用ですが、コンシューマーはこれらの行セットが公開するインターフェイスを使用することで、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルの構造を決定できます。 一括コピー可能な [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダー行セットは、次のインターフェイスを公開します。  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
-   **IColumnsRowset**  
  
-   **IConvertType**  
  
-   **IRowsetFastLoad**  
  
-   **IRowsetInfo**  
  
-   **ISupportErrorInfo**  
  
 プロバイダー固有のプロパティ SSPROP_FASTLOADOPTIONS、SSPROP_FASTLOADKEEPNULLS、および SSPROP_FASTLOADKEEPIDENTITY により、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーの一括コピー行セットの動作が制御されます。 プロパティは、 _rgPropertySets_**IOpenRowset**parameter メンバーの*rgProperties*メンバーに指定されています。  
  
|プロパティ ID|[説明]|  
|-----------------|-----------------|  
|SSPROP_FASTLOADKEEPIDENTITY|列 : なし<br /><br /> R/W: 読み取り/書き込み<br /><br /> 型 : VT_BOOL<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明 : コンシューマーが指定する ID 値を管理します。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] テーブルの ID 列の値が [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] によって生成されます。 列にバインドされている値は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーによって無視されます。<br /><br /> VARIANT_TRUE: コンシューマーが、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ID 列に値を提供するアクセサーをバインドします。 NULL を許容する列では ID プロパティを使用できないので、コンシューマーは **IRowsetFastLoad::Insert** を呼び出すたびに一意な値を指定します。|  
|SSPROP_FASTLOADKEEPNULLS|列 : なし<br /><br /> R/W: 読み取り/書き込み<br /><br /> 型 : VT_BOOL<br /><br /> 既定値 : VARIANT_FALSE<br /><br /> 説明 : DEFAULT 制約が適用されている列の NULL 値を管理します。 影響を受けるのは、NULL 値を許容し、DEFAULT 制約が適用されている [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列だけです。<br /><br /> VARIANT_FALSE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーが列に NULL 値を含む行を挿入すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではその列に既定値が挿入されます。<br /><br /> VARIANT_TRUE: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーのコンシューマーが列に NULL 値を含む行を挿入すると、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ではその列に NULL 値が挿入されます。|  
|SSPROP_FASTLOADOPTIONS|列 : なし<br /><br /> R/W: 読み取り/書き込み<br /><br /> 型 : VT_BSTR<br /><br /> 既定値 : なし<br /><br /> 説明 : このプロパティは、**bcp** ユーティリティの *-h* "*hint*[,...**n**]" オプションと同じです。 データをテーブルに一括コピーするときのオプションとして、次の文字列を使用できます。<br /><br /> **ORDER**(*column*[**ASC** &#124; **DESC**][,...*n*]): データ ファイル内のデータの並べ替え順です。 読み込むデータ ファイルをテーブル上のクラスター化インデックスに従って並べ替えると、一括コピーのパフォーマンスが向上します。<br /><br /> **ROWS_PER_BATCH** = *bb*: バッチあたりのデータの行数です (*bb*)。 サーバーは、*bb* の値に応じて一括コピーの負荷を最適化します。 **ROWS_PER_BATCH** の既定値はありません。<br /><br /> **KILOBYTES_PER_BATCH** = *cc*: バッチごとのデータの KB (キロバイト数) です (cc)。 **KILOBYTES_PER_BATCH** の既定値はありません。<br /><br /> **TABLOCK**: 一括コピー操作時にテーブルレベルのロックを行います。 一括コピー操作中だけロックを保持することにより、テーブル ロックの競合が少なくなるので、このオプションによりパフォーマンスが大幅に向上します。 テーブルにインデックスがなく、**TABLOCK** が指定されている場合は、複数のクライアントが同時に 1 つのテーブルを読み込むことができます。 既定では、ロック動作はテーブル オプション **table lock on bulk load** によって決定されます。<br /><br /> **CHECK_CONSTRAINTS**: 一括コピー操作中、*table_name* に適用されているすべての制約がチェックされます。 既定では、制約は無視されます。<br /><br /> **FIRE_TRIGGER**: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] では、トリガーに対して行のバージョン管理が使用され、行のバージョンが **tempdb** 内のバージョン ストアに格納されます。 したがって、トリガーが有効になっていても一括ログ記録を最適化できます。 トリガーを有効にして大量の行が含まれるバッチを一括インポートする前に、**tempdb** のサイズの拡張が必要になる場合があります。|  
  
### <a name="using-file-based-bulk-copy-operations"></a>ファイル ベースの一括コピー操作の使用  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB プロバイダーは、 **Ibcpsession**インターフェイスを実装して [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ファイルベースの一括コピー操作のサポートを公開します。 **IBCPSession** インターフェイスには、[IBCPSession::BCPColFmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolfmt-ole-db.md)、[IBCPSession::BCPColumns](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcolumns-ole-db.md)、[IBCPSession::BCPControl](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpcontrol-ole-db.md)、[IBCPSession::BCPDone](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpdone-ole-db.md)、[IBCPSession::BCPExec](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpexec-ole-db.md)、[IBCPSession::BCPInit](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpinit-ole-db.md)、[IBCPSession::BCPReadFmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpreadfmt-ole-db.md)、および [IBCPSession::BCPWriteFmt](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-bcpwritefmt-ole-db.md) の各メソッドが実装されます。  
  
## <a name="sql-server-native-client-odbc-driver"></a>SQL Server Native Client ODBC ドライバー  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、以前のバージョンの [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ODBC ドライバーの一部であった一括コピー操作サポートが同様に提供されます。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーを使用した一括コピー操作の詳細については、「[一括コピー操作&#40;の実行 (odbc&#41;](../../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md))」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client の機能](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [データ ソースのプロパティ &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-properties-ole-db.md)   
 [データの一括インポートと一括エクスポート &#40;SQL Server&#41;](../../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [IRowsetFastLoad &#40;OLE DB&#41; ](../../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-ole-db.md)   
 [Ibcpsession &#40;OLE DB&#41; ](../../../relational-databases/native-client-ole-db-interfaces/ibcpsession-ole-db.md)   
 [一括インポートのパフォーマンスの最適化](https://msdn.microsoft.com/library/ms190421\(SQL.105\).aspx)  
  
  
