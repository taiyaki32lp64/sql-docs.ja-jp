---
title: データ型の使用量 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data types
- ODBC data types, about ODBC data types
- SQL Server Native Client ODBC driver, result sets
- ODBC applications, result sets
- data types [ODBC]
- SQL Server Native Client ODBC driver, data types
- data types [ODBC], about data types
ms.assetid: 4f19b0d6-94ac-4a98-a121-57d38787864c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 170cbfffde1b28d60617f0e0166ca9f8e31f5fb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200185"
---
# <a name="data-type-usage"></a>データ型の使用方法
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーと[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型の次の使用を強制します。  
  
|データ型|制限事項|  
|---------------|----------------|  
|日付リテラル|Sql_type_timestamp 型の列に格納されているときの日付リテラル ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータ型**datetime**または**smalldatetime**)、12:00:00.000 a.m ですの時刻の値がある。|  
|**money**と**smallmoney**|整数部分のみ、 **money**と**smallmoney**データ型が重要です。 場合は SQL の小数部**money**データ型の変換中にデータが切り捨てられます、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは警告をエラーではなくを返します。|  
|SQL_BINARY (NULL 値を許容)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 以前のインスタンスに接続していて、SQL_BINARY 型の列で NULL 値が許容される場合、データ ソースに格納されているデータには 0 が埋め込まれません。 このような列からデータを取得するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが右側に表示されるゼロを埋め込みます。 ただし、連結など、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により実行される操作で作成されるデータには、このような埋め込みは行われません。<br /><br /> また、データを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 以前のインスタンスの列に格納するときに、そのデータが長すぎて列に収まりきらない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はデータを右側から切り捨てます。 **注:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはへの接続をサポートして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 およびそれ以前。|  
|SQL_CHAR (切り捨て)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 以前のインスタンスに接続し、データを SQL_CHAR 型の列に格納するときに、そのデータが長すぎて列に収まりきらない場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では警告を通知せずにデータを右側から切り捨てます。 **注:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはへの接続をサポートして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 およびそれ以前。|  
|SQL_CHAR (NULL 値を許容)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 6.0 以前のインスタンスに接続していて、SQL_CHAR 型の列で NULL 値が許容される場合、データ ソースに格納されているデータには空白が埋め込まれません。 このような列からデータを取得するとき、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーが右側の空白を埋め込みます。 ただし、連結など、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により実行される操作で作成されるデータには、このような埋め込みは行われません。 **注:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはへの接続をサポートして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 およびそれ以前。|  
|SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR|インスタンスに接続しているときに、SQL_LONGVARBINARY、SQL_LONGVARCHAR、SQL_WLONGVARCHAR データ型の列 (WHERE 句を使用して) 複数の行に影響を与えるの更新プログラムが完全にサポートされて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6 *。x*以降。 インスタンスに接続されているときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*、S1000 エラー、"部分的な挿入または更新します。 text または image 列の挿入または更新に失敗しました。" が返されます。 **注:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはへの接続をサポートして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 およびそれ以前。|  
|文字列関数パラメーター|*string_exp* SQL_CHAR、SQL_VARCHAR またはデータの関数があります。 文字列にパラメーターが入力されます。 SQL_LONG_VARCHAR データ型はサポートされません。 *カウント*パラメーター SQL_CHAR、SQL_VARCHAR データ型は 8,000 文字の最大の長さに制限ができないために 8,000 以下にする必要があります。|  
|時刻リテラル|Sql_timestamp 型の列に格納されているときの時刻リテラル ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のデータ型**datetime**または**smalldatetime**)、1900 年 1 月 1 日の日付値を指定します。|  
|**timestamp**|NULL 値のみを手動で挿入できる、**タイムスタンプ**列。 ただし、ため**タイムスタンプ**列はによって自動的に更新[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]NULL 値が上書きされます。|  
|**tinyint**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Tinyint**データ型が符号なし。 A **tinyint**列は、既定では SQL_C_UTINYINT データ型の変数にバインドされます。|  
|別名データ型|インスタンスに接続されているときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*、ODBC ドライバーは、列の null 値の許容を明示的に宣言しない列の定義に NULL を追加します。 したがって、別名データ型の定義に格納されている NULL 値の許容属性は無視されます。<br /><br /> インスタンスに接続されているときに[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]4.2*x*の基本データを持つ、別名データ型の列が入力**char**または**バイナリ**と、null 値許容属性はありません宣言は、データ型として作成**varchar**または**varbinary**します。 [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md)、 [SQLColumns](../native-client-odbc-api/sqlcolumns.md)、および[SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md)戻り値として SQL_VARCHAR または SQL_VARBINARY、データのこれらの列を入力します。 これらの列から取得するデータには、埋め込みは行われません。 **注:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはへの接続をサポートして[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]6.5 およびそれ以前。|  
|LONG データ型|*実行時データ*パラメーターは、SQL_LONGVARBINARY、SQL_LONGVARCHAR データ型の両方に制限されます。|  
|大きな値型|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーは、公開**varchar (max)** 、 **varbinary (max)** 、および**nvarchar (max)** 型として SQL_VARCHAR、SQL_VARBINARY、および sql _WVARCHAR (それぞれ) Api で ODBC SQL データ型を返します。|  
|ユーザー定義型 (UDT)|UDT 列は SQL_SS_UDT としてマップされます。 SQL ステートメントで、UDT の ToString() メソッドまたは ToXMLString() メソッドを使用するか、CAST/CONVERT 関数を使用して UDT 列を明示的に別の型にマップする場合、結果セット内の列の型には変換された列の実際の型が反映されます。<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーはバイナリとしての UDT 列にのみバインドできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でサポートされるのは、SQL_SS_UDT データ型と SQL_C_BINARY データ型の間の変換のみです。|  
|XML|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、XML を Unicode テキストに自動的に変換します。 XML 型は SQL_SS_XML としてマップされます。|  
  
## <a name="see-also"></a>関連項目  
 [結果の処理&#40;ODBC&#41;](processing-results-odbc.md)  
  
  
