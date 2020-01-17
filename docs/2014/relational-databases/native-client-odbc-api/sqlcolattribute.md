---
title: SQLColAttribute |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLColAttribute function
ms.assetid: a5387d9e-a243-4cfe-b786-7fad5842b1d6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 706d08eb3c140571460f4ebccb541ac24a71160a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63067676"
---
# <a name="sqlcolattribute"></a>SQLColAttribute
  使用することができます`SQLColAttribute`準備または実行された ODBC ステートメントの結果セット列の属性を取得します。 呼び出す`SQLColAttribute`で準備されたステートメント原因へのラウンドト リップ[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、呼び出すので、ステートメントの実行の一部として結果セット列のデータを受信`SQLColAttribute`の完了後**SQLExecute**または**SQLExecDirect**はサーバーとのやり取りは関係ありません。  
  
> [!NOTE]  
>  すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の結果セットで、ODBC 列の ID 属性は使用できません。  
  
|フィールド ID|説明|  
|----------------------|-----------------|  
|SQL_COLUMN_TABLE_NAME|サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。|  
|SQL_DESC_BASE_COLUMN_NAME|サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。|  
|SQL_DESC_BASE_TABLE_NAME|サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。|  
|SQL_DESC_CATALOG_NAME|データベース名。 サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。|  
|SQL_DESC_LABEL|すべての結果セットで使用できます。 値は、SQL_DESC_NAME フィールドの値と等しくなります。<br /><br /> 列が式の結果か、式にラベル割り当てが含まれていない場合にのみ、フィールド長が 0 (ゼロ) になります。|  
|SQL_DESC_NAME|すべての結果セットで使用できます。 値は、SQL_DESC_LABEL フィールドの値と等しくなります。<br /><br /> 列が式の結果か、式にラベル割り当てが含まれていない場合にのみ、フィールド長が 0 (ゼロ) になります。|  
|SQL_DESC_SCHEMA_NAME|所有者名。 サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。<br /><br /> SELECT ステートメントの列に所有者名を指定した場合にのみ使用できます。|  
|SQL_DESC_TABLE_NAME|サーバー カーソルを生成するステートメントから取得した結果セットで使用できます。または、FOR BROWSE 句を含む実行済みの SELECT ステートメントで使用できます。|  
|SQL_DESC_UNNAMED|結果セット内にあるすべての列に対する SQL_NAMED が返されます。ただしこれは、式の一部にラベル割り当てが含まれておらず、列がこの式の結果ではない場合に限ります。 SQL_DESC_UNNAMED が SQL_UNNAMED を返すときは、すべての ODBC 列の ID 属性には、その列に対して長さゼロの文字列が含まれます。|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーでは、SET FMTONLY ステートメントを使用して、サーバーのオーバーヘッドを減らすとき`SQLColAttribute`が呼び出されると準備されたステートメントが実行されていません。  
  
 大きな値型、`SQLColAttribute`は次の値を返します。  
  
|フィールド ID|変更の説明|  
|----------------------|---------------------------|  
|SQL_DESC_DISPLAY_SIZE|列のデータを表示する場合に必要となる最大文字数です。 大きな値型の列の場合、返される値は SQL_SS_LENGTH_UNLIMITED です。|  
|SQL_DESC_LENGTH|結果セット内の列の実際の長さを返します。 大きな値型の列の場合、返される値は SQL_SS_LENGTH_UNLIMITED です。|  
|SQL_DESC_OCTET_LENGTH|大きな値型の列の最大長を返します。 無制限のサイズを示す場合、SQL_SS_LENGTH_UNLIMITED を使用します。|  
|SQL_DESC_PRECISION|大きな値型の列の場合、値 SQL_SS_LENGTH_UNLIMITED を返します。|  
|SQL_DESC_TYPE|大きな値型の場合、SQL_VARCHAR、SQL_WVARCHAR、および SQL_VARBINARY を返します。|  
|SQL_DESC_TYPE_NAME|大きな値型の場合、"varchar"、"varbinary"、"nvarchar" を返します。|  
  
 すべてのバージョンで、準備された SQL ステートメントのバッチによって複数の結果セットが生成されるときは、最初の結果セットのみの列属性が報告されます。  
  
 次の列属性は、拡張機能によって公開されている、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバー。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、すべての値を返します、 *NumericAttrPtr*パラメーター。 WORD 配列へのポインターである SQL_CA_SS_COMPUTE_BYLIST を除き、SDWORD 型 (符号付き long 型) として値が返されます。  
  
|フィールド ID|返される値|  
|----------------------|--------------------|  
|SQL_CA_SS_COLUMN_HIDDEN*|参照される列が、FOR BROWSE 句を含む Transact-SQL SELECT ステートメントをサポートするために作成された非表示の主キーの一部である場合は、TRUE になります。|  
|SQL_CA_SS_COLUMN_ID|現在の Transact-SQL SELECT ステートメント内にある COMPUTE 句の結果列の序数位置。|  
|SQL_CA_SS_COLUMN_KEY*|参照される列が行の主キーの一部で、Transact-SQL SELECT ステートメントに FOR BROWSE 句が含まれる場合は、TRUE になります。|  
|SQL_CA_SS_COLUMN_OP|COMPUTE 句列の値に関連する集計演算子を指定する整数。 整数値の定義は sqlncli.h にあります。|  
|SQL_CA_SS_COLUMN_ORDER|ODBC または Transact-SQL SELECT ステートメントの ORDER BY 句内にある列の序数位置。|  
|SQL_CA_SS_COLUMN_SIZE|列から取得したデータ値を SQL_C_BINARY 変数にバインドするのに必要な、バイト単位の最大長。|  
|SQL_CA_SS_COLUMN_SSTYPE|SQL Server の列に格納されたデータのネイティブ データ型。 型値の定義は sqlncli.h にあります。|  
|SQL_CA_SS_COLUMN_UTYPE|SQL Server における列のユーザー定義データ型に関する基本データ型。 型値の定義は sqlncli.h にあります。|  
|SQL_CA_SS_COLUMN_VARYLEN|列のデータが可変長の場合は TRUE、それ以外の場合は FALSE です。|  
|SQL_CA_SS_COMPUTE_BYLIST|COMPUTE 句の BY 句で使用される列を指定する、WORD 型 (符号なし short 型) の配列へのポインター。 COMPUTE 句に BY が指定されていない場合、NULL ポインターを返します。<br /><br /> 配列の最初の要素には、BY リスト列の数が含まれます。 もう 1 つの要素は列序数です。|  
|SQL_CA_SS_COMPUTE_ID|*computeid*の現在の TRANSACT-SQL SELECT ステートメントの COMPUTE 句の結果である行のできます。|  
|SQL_CA_SS_NUM_COMPUTES|現在の Transact-SQL SELECT ステートメントで指定されている COMPUTE 句の数。|  
|SQL_CA_SS_NUM_ORDERS|ODBC または Transact-SQL SELECT ステートメントの ORDER BY 句で指定されている列の数。|  
  
 \*   ステートメント属性 SQL_SOPT_SS_HIDDEN_COLUMNS を SQL_HC_ON に設定されている場合は使用できます。  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] XML スキーマ コレクションの名前、スキーマ名、およびカタログの名前をそれぞれ示す追加情報を提供するドライバー固有の記述子フィールドが導入されました。 これらのプロパティでは、英数字以外の文字が含まれる場合でも、引用符やエスケープ文字は必要ありません。 次の表では、追加された新しい記述子フィールドについて説明します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_CATALOG_NAME|CharacterAttributePtr|XML スキーマ コレクション名が定義されているカタログの名前です。 カタログ名が見つからない場合は、この変数に空文字列が含まれます。<br /><br /> この情報は、IRD の SQL_DESC_SS_XML_SCHEMACOLLECTION_CATALOG_NAME レコード フィールドから返されます。このレコード フィールドは読み取りと書き込みが可能なフィールドです。|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_SCHEMA_NAM E|CharacterAttributePtr|XML スキーマ コレクション名が定義されているスキーマの名前です。 スキーマ名が見つからない場合は、この変数に空文字列が含まれます。<br /><br /> この情報は、IRD の SQL_DESC_SS_XML_SCHEMACOLLECTION_SCHEMA_NAME レコード フィールドから返されます。このレコード フィールドは読み取りと書き込み可能なフィールドです。|  
|SQL_CA_SS_XML_SCHEMACOLLECTION_NAME|CharacterAttributePtr|XML スキーマ コレクションの名前です。 名前が見つからない場合は、この変数に空文字列が含まれます。<br /><br /> この情報は、IRD の SQL_DESC_SS_XML_SCHEMACOLLECTION_NAME レコード フィールドから返されます。このレコード フィールドは読み取りと書き込み可能なフィールドです。|  
  
 また、[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] では、結果セットのユーザー定義型 (UDT) 列に関する追加情報、またはストアド プロシージャやパラメーター化クエリの UDT パラメーターに関する追加情報を提供するために、ドライバー固有の新しい記述子フィールドが導入されました。 これらのプロパティでは、英数字以外の文字が含まれる場合でも、引用符やエスケープ文字は必要ありません。 次の表では、追加された新しい記述子フィールドについて説明します。  
  
|列名|型|説明|  
|-----------------|----------|-----------------|  
|SQL_CA_SS_UDT_CATALOG_NAME|CharacterAttributePtr|UDT を含むカタログの名前。|  
|SQL_CA_SS_UDT_SCHEMA_NAME|CharacterAttributePtr|UDT を含むスキーマの名前。|  
|SQL_CA_SS_UDT_TYPE_NAME|CharacterAttributePtr|UDT の名前|  
|SQL_CA_SS_UDT_ASSEMBLY_TYPE_NAME|CharacterAttributePtr|UDT のアセンブリ修飾名。|  
  
 UDT の名前を示すために、既存の記述子フィールド ID の SQL_DESC_TYPE_NAME が使用されます。 UDT 型の列の SQL_DESC_TYPE フィールドは SQL_SS_UDT です。  
  
## <a name="sqlcolattribute-support-for-enhanced-date-and-time-features"></a>SQLColAttribute による機能強化された日付と時刻のサポート  
 日付/時刻型に対して返される値、「情報が返されます IRD フィールドで」のセクションを参照してください。[パラメーターと結果のメタデータ](../native-client-odbc-date-time/metadata-parameter-and-result.md)します。  
  
 詳細については、次を参照してください。[日付と時刻の強化&#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)します。  
  
## <a name="sqlcolattribute-support-for-large-clr-udts"></a>SQLColAttribute による大きな CLR UDT のサポート  
 `SQLColAttribute` は、大きな CLR ユーザー定義型 (UDT) をサポートしています。 詳細については、次を参照してください。 [Large CLR User-Defined 型&#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md)します。  
  
## <a name="sqlcolattribute-support-for-sparse-columns"></a>SQLColAttribute によるスパース列のサポート  
 Sqlcolattribute によるクエリを新しい実装行記述子 (IRD) フィールド SQL_CA_SS_IS_COLUMN_SET、列が決定する、`column_set`列。  
  
 詳細については、次を参照してください。[スパース列のサポート&#40;ODBC&#41;](../native-client/odbc/sparse-columns-support-odbc.md)します。  
  
## <a name="see-also"></a>参照  
 [SQLColAttribute 関数](https://go.microsoft.com/fwlink/?LinkId=59334)   
 [ODBC API 実装の詳細](odbc-api-implementation-details.md)   
 [SQLSetStmtAttr](sqlsetstmtattr.md)  
  
  
