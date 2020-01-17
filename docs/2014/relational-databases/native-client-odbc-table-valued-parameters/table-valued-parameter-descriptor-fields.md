---
title: テーブル値パラメーターの記述子フィールド |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (ODBC), descriptor fields
ms.assetid: 4e009eff-c156-4d63-abcf-082ddd304de2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd58bdb611a070c812364baf2fa3e1544c2ffdc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63228963"
---
# <a name="table-valued-parameter-descriptor-fields"></a>テーブル値パラメーターの記述子フィールド
  テーブル値パラメーターのサポートには、ODBC アプリケーション パラメーター記述子 (APD) および実装パラメーター記述子 (IPD) の新しい [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有のフィールドが含まれます。  
  
## <a name="remarks"></a>コメント  
  
|名前|場所|型|説明|  
|----------|--------------|----------|-----------------|  
|SQL_CA_SS_TYPE_NAME|IPD|SQLTCHAR*|テーブル値パラメーターのサーバーの型名です。<br /><br /> SQLBindParameter への呼び出しで、テーブル値パラメーターの型名を指定すると、ANSI アプリケーションとしてビルドされているアプリケーションも Unicode 値として常に指定する必要があります。 パラメーターに使用される値*StrLen_or_IndPtr* SQL_NTS または sizeof (wchar) を掛けた値名の文字列の長さのいずれかにする必要があります。<br /><br /> テーブル値パラメーターの型名を指定した場合、SQLSetDescField を使用して、アプリケーションに準拠する方法は、リテラルを使用して指定できますが構築されています。 ODBC ドライバー マネージャーで、必要な Unicode 変換を実行します。|  
|SQL_CA_SS_TYPE_CATALOG_NAME (読み取り専用)|IPD|SQLTCHAR*|型が定義されているカタログです。|  
|SQL_CA_SS_TYPE_SCHEMA_NAME|IPD|SQLTCHAR*|型が定義されているスキーマです。|  
  
 アプリケーションでは、テーブル値パラメーターの SQL_CA_SS_TYPE_CATALOG_NAME を設定できません。 これを設定すると、SQL_ERROR が返され、"記述子フィールドの識別子が正しくありません" というメッセージで SQLSTATE = HY091 の診断レコードが記録されます。  
  
 次のステートメント属性および記述子のヘッダー フィールドは、テーブル値パラメーターにフォーカスが設定されている場合に適用されます。  
  
|名前|場所|型|説明|  
|----------|--------------|----------|-----------------|  
|SQL_ATTR_PARAMSET_SIZE<br /><br /> (APD の SQL_DESC_ARRAY_SIZE に相当)|APD|SQLUINTEGER|テーブル値パラメーターのバッファー配列のサイズです。 これは、バッファーが保持できる最大行数、または行内のバッファーのサイズです。テーブル値パラメーターの値自体には、バッファーで保持できるよりも多い (または少ない) 行が含まれる場合があります。 既定値は 1 です。 **注:** SQL_SOPT_SS_PARAM_FOCUS が 0 の既定値に設定されている場合 SQL_ATTR_PARAMSET_SIZE はステートメントを参照し、パラメーター セットの数を指定します。 SQL_SOPT_SS_PARAM_FOCUS がテーブル値パラメーターの序数に設定されている場合は、テーブル値パラメーターを参照し、テーブル値パラメーターのパラメーター セットごとの行数を指定します。|  
|SQL_ATTR_PARAM _BIND_TYPE|APD|SQLINTEGER|既定値は SQL_PARAM_BIND_BY_COLUMN です。<br /><br /> 行方向のバインドを選択するには、このフィールドに、構造体の長さ、または一連のテーブル値パラメーターの行のバインドされるバッファーのインスタンスの長さが設定されます。 この長さには、バインドされたすべての列の領域と、構造体またはバッファーの埋め込みを含める必要があります。 これにより、バインドされた列のアドレスが指定の長さでインクリメントされると、結果は、次の行の同じ列の先頭を指すようになります。 ANSI C の `sizeof` 演算子を使用すると、この動作が保証されます。|  
|SQL_ATTR_PARAM_BIND_OFFSET_PTR|APD|SQLINTEGER*|既定値は NULL ポインターです。<br /><br /> このフィールドが NULL 以外の場合、ドライバーはポインターを逆参照し、逆参照された値を記述子レコードの遅延された各フィールド (SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、および SQL_DESC_OCTET_LENGTH_PTR) に追加して、新しいポインター値を使用してデータ値にアクセスします。|  
  
 これらのフィールドは、テーブル値パラメーターでのみ有効です。それ以外のデータ型の場合は無視されます。  
  
 ストアド プロシージャを呼び出す場合、SQL_CA_SS_TYPE_NAME は省略可能です。 サーバー側でテーブル値パラメーターの型を特定できるようなプロシージャの呼び出しでない場合は、SQL ステートメントで SQL_CA_SS_TYPE_NAME を指定する必要があります。  
  
 型名が必要で、テーブル値パラメーターのテーブル型がストアド プロシージャとは異なるスキーマで定義されている場合、SQL_CA_SS_TYPE_SCHEMA_NAME を実装パラメーター記述子 (IPD) で指定する必要があります。 指定しないと、サーバーでテーブル値パラメーターの型を特定できません。 これは、エラーが発生、SQLExecute または SQLExecDirect を呼び出すとします。 エラーは SQLSTATE= 07006 で、メッセージは "データ型の属性に関する制限に違反しました" になります。  
  
 テーブル値パラメーターの列では、行方向のバインドまたは列方向のバインドを使用できます。 既定では、列方向のバインドが使用されます。 行方向のバインドは、SQL_ATTR_PARAM_BIND_TYPE および SQL_ATTR_ PARAM_BIND_OFFSET_PTR を設定することで指定できます。 これは、列およびパラメーターの行方向のバインドと似ています。  
  
 SQL_CA_SS_TYPE_CATALOG_NAME および SQL_CA_SS_TYPE_SCHEMA_NAME を使用すると、CLR ユーザー定義型パラメーターに関連付けられたカタログとスキーマも取得できます。 これらは、CLR ユーザー定義型の既存の型固有のカタログ スキーマの属性の代わりに使用します。  
  
## <a name="see-also"></a>関連項目  
 [テーブル値パラメーター &#40;ODBC&#41;](table-valued-parameters-odbc.md)  
  
  
