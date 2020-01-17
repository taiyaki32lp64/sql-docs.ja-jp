---
title: SQL Server Native Client | でのスパース列のサポートMicrosoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- sparse columns, ODBC
- sparse columns, SQL Server Native Client
- sparse columns, OLE DB
ms.assetid: aee5ed81-7e23-42e4-92d3-2da7844d9bc3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21b79a06acd838278073dee58026269f63b0da04
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75231710"
---
# <a name="sparse-columns-support-in-sql-server-native-client"></a>SQL Server Native Client におけるスパース列のサポート
  
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client はスパース列をサポートしています。 の[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]スパース列の詳細については、「[スパース列の使用](../../tables/use-sparse-columns.md)」および「[列セットの使用](../../tables/use-column-sets.md)」を参照してください。  
  
 Native Client で[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]のスパース列のサポートの詳細については、「スパース列の[サポート &#40;ODBC&#41;](../odbc/sparse-columns-support-odbc.md) 」と「[スパース列での &#40;OLE DB の&#41;](../ole-db/sparse-columns-support-ole-db.md)のサポート」を参照してください。  
  
 この機能を説明するサンプル アプリケーションについては、「[SQL Server データ プログラミング サンプル](https://msftdpprodsamples.codeplex.com/)」を参照してください。  
  
## <a name="user-scenarios-for-sparse-columns-and-sql-server-native-client"></a>スパース列と SQL Server Native Client のユーザー シナリオ  
 スパース列を使用する [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ユーザーの一般的なユーザー シナリオの概要を次の表に示します。  
  
|シナリオ|動作|  
|--------------|--------------|  
|**select \* from Table**または IOpenRowset:: OpenRowset。|スパース `column_set` のメンバーでないすべての列と、スパース `column_set` のメンバーであるすべての NULL 以外の列の値を含む XML 列が返されます。|  
|名前で列を参照する。|スパース列かどうか、`column_set` のメンバーかどうかに関係なく、列を参照できます。|  
|XML 計算列を通じて `column_set` メンバー列にアクセスする。|スパース `column_set` のメンバーである列に、名前で `column_set` を選択してアクセスし、`column_set` 列の XML を更新して値を挿入および更新できます。<br /><br /> 値は、`column_set` 列のスキーマに準拠している必要があります。|  
|列検索パターンが NULL または '% ' の SQLColumns を使用して、テーブル内のすべての列のメタデータを取得します (ODBC)。または、列の制限のない DBSCHEMA_COLUMNS スキーマ行セット (OLE DB) を使用します。|
  `column_set` のメンバーでないすべての列について 1 つの行が返されます。 テーブルにスパース `column_set` がある場合は、そのスパース  について 1 つの行が返されます。<br /><br /> この場合、`column_set` のメンバーである列のメタデータは返されないことに注意してください。|  
|スパース列かどうか、`column_set` のメンバーかどうかに関係なく、すべての列のメタデータを取得する。 この場合、大量の行が返される可能性があります。|記述子フィールド SQL_SOPT_SS_NAME_SCOPE を SQL_SS_NAME_SCOPE_EXTENDED に設定し、 [Sqlcolumns](../../native-client-odbc-api/sqlcolumns.md) (ODBC) を呼び出します。<br /><br /> DBSCHEMA_COLUMNS_EXTENDED スキーマ行セット (OLE DB) に対して IDBSchemaRowset:: GetRowset を呼び出します。<br /><br /> このシナリオは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のリリースの [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client を使用するアプリケーションでは使用できません。 ただし、そのようなアプリケーションでは、直接システム ビューに対してクエリを実行できます。|  
|
  `column_set` のメンバーである列についてのみメタデータを取得する。 この場合、大量の行が返される可能性があります。|記述子フィールド SQL_SOPT_SS_NAME_SCOPE を SQL_SS_NAME_SCOPE_SPARSE_COLUMN_SET に設定し、SQLColumns (ODBC) を呼び出します。<br /><br /> DBSCHEMA_SPARSE_COLUMN_SET スキーマ行セット (OLE DB) に対して IDBSchemaRowset:: GetRowset を呼び出します。<br /><br /> このシナリオは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のリリースの [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client を使用するアプリケーションでは使用できません。 ただし、そのようなアプリケーションでは、システム ビューに対してクエリを実行できます。|  
|列がスパース列かどうかを確認する。|SQLColumns 結果セット (ODBC) の SS_IS_SPARSE 列を参照してください。<br /><br /> DBSCHEMA_COLUMNS スキーマ行セットの SS_IS_SPARSE 列を調べます (OLE DB)。<br /><br /> このシナリオは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のリリースの [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client を使用するアプリケーションでは使用できません。 ただし、そのようなアプリケーションでは、システム ビューに対してクエリを実行できます。|  
|列が `column_set` かどうかを確認する。|SQLColumns 結果セットの SS_IS_COLUMN_SET 列を参照してください。 または、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 固有の列属性である SQL_CA_SS_IS_COLUMN_SET を調べます (ODBC)。<br /><br /> DBSCHEMA_COLUMNS スキーマ行セットの SS_IS_COLUMN_SET 列を調べます。 または、IColumnsRowset:: GetColumnsRowset によって返された行セットの IColumnsinfo:: GetColumnInfo または DBCOLUMNFLAGS によって返された*dwFlags*を参照してください。 
  `column_set` 列の場合は DBCOLUMNFLAGS_SS_ISCOLUMNSET が設定されます (OLE DB)。<br /><br /> このシナリオは、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] より前のリリースの [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] Native Client を使用するアプリケーションでは使用できません。 ただし、そのようなアプリケーションでは、システム ビューに対してクエリを実行できます。|  
|
  `column_set` を含まないテーブルに対して BCP でスパース列をインポートおよびエクスポートする。|
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の以前のバージョンから動作は変更されていません。|  
|
  `column_set` を含むテーブルに対して BCP でスパース列をインポートおよびエクスポートする。|は`column_set` 、XML と同じ方法でインポートおよびエクスポートされます。これは、バイナリ`varbinary(max)`型としてバインドされている`nvarchar(max)`場合と同様に`char` 、または**wchar**型としてバインドされている場合と同様です。<br /><br /> スパース `column_set` のメンバーである列は個別の列としてはエクスポートされず、`column_set` の値でのみエクスポートされます。|  
|BCP の `queryout` の動作。|明示的に指定された列の処理は、[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client の以前のバージョンから変更されていません。<br /><br /> スキーマが異なる列の間のインポートおよびエクスポートを含むシナリオでは、特別な処理が必要になる場合があります。<br /><br /> BCP の詳細については、後の「一括コピー (BCP) によるスパース列のサポート」を参照してください。|  
  
## <a name="down-level-client-behavior"></a>下位クライアントの動作  
 ダウンレベルクライアントは、SQLColumns および DBSCHMA_COLUMNS のスパース`column_set`のメンバーでない列に対してのみメタデータを返します。 Native Client で[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]導入された追加の OLE DB スキーマ行セットは使用できません。また、ODBC の sqlcolumns は SQL_SOPT_SS_NAME_SCOPE を使用して変更されることもありません。  
  
 下位クライアントでは、スパース `column_set` のメンバーである列に名前でアクセスできます。`column_set` クライアントでは XML 列として [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 列にアクセスできます。  
  
## <a name="bulk-copy-bcp-support-for-sparse-columns"></a>一括コピー (BCP) によるスパース列のサポート  
 ODBC および OLE DB の BCP API には、スパース列や `column_set` 機能のための変更はありません。  
  
 テーブルに `column_set` がある場合、スパース列は個別の列として処理されません。 すべてのスパース列の値は、 `column_set`XML 列と同じ方法でエクスポートされるの値に含まれます。これは、バイナリ`varbinary(max)`型としてバインドされている`nvarchar(max)`かのように`char` 、またはまたは**wchar**型としてバインドされているかのようになります。 インポートの際には、`column_set` の値が `column_set` のスキーマに準拠している必要があります。  
  
 
  `queryout` の操作については、明示的に参照されている列の処理方法は変更されていません。 
  `column_set` 列の動作は XML 列と同じで、名前で参照されているスパース列の処理には、列がスパース列であることの影響はありません。  
  
 ただし、`queryout` をエクスポートに使用する場合に、スパース列セットのメンバーであるスパース列を名前で参照すると、同じ構造のテーブルへの直接インポートを実行できなくなります。 これは、BCP がインポートの**select \* **操作と一貫性のあるメタデータを使用し、 `column_set`メンバー列をこのメタデータと一致させることができないためです。 
  `column_set` メンバー列を個別にインポートするには、目的の `column_set` 列を参照するテーブルのビューを定義して、そのビューを使用してインポート操作を実行する必要があります。  
  
## <a name="see-also"></a>参照  
 [SQL Server Native Client プログラミング](../sql-server-native-client-programming.md)  
  
