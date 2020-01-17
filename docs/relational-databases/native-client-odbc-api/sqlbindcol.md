---
title: SQLBindCol |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a92c95a67b6e9fd3d31917af4f5b7b19f4c613d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787792"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  一般的な規則として、 **SQLBindCol**を使用してデータ変換を行う場合の影響について検討します。 バインドによる変換はクライアント側のプロセスなので、たとえば文字型の列にバインドされた浮動小数点値を取得すると、ドライバーは行をフェッチするときにローカルで浮動小数点型から文字型への変換を行います。 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 関数を使用すると、データ変換の負荷をサーバーに移すことができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスでは、1 回のステートメントの実行に対して複数の結果セット行を返すことができます。 各結果セットは個別にバインドされている必要があります。 複数の結果セットのバインドの詳細については、「 [Sqlmoreresults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)」を参照してください。  
  
 開発者は、 *TargetType*値**SQL_C_BINARY**を使用して、列を [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]固有の C データ型にバインドできます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の型にバインドされた列は移植できません。 また、定義済みの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 固有の ODBC C データ型は DB-Library の型定義と一致するので、アプリケーションを移植する DB-Library 開発者はこの特性を利用できます。  
  
 レポートデータの切り捨ては、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC ドライバーにとってコストのかかるプロセスです。 バインドされるすべてのデータ バッファーのサイズがデータを返すのに十分なサイズであれば、データの切り捨てを回避できます。 文字データの場合、文字列の終了に既定のドライバーの動作を使用するときは、データ バッファーの大きさに文字列ターミネータの領域も含める必要があります。 たとえば、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char (5)** 列を5文字の配列にバインドすると、フェッチされるすべての値が切り捨てられます。 同じ列を 6 文字の配列にバインドすると、NULL ターミネータを格納する文字要素が用意されるため、切り捨てを回避できます。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)を使用すると、長い文字とバイナリデータを切り捨てずに効率的に取得できます。  
  
 大きな値のデータ型の場合、ユーザーが指定したバッファーのサイズが列の値全体を保持するのに十分ではない場合、 **SQL_SUCCESS_WITH_INFO**が返され、"文字列データ;"右切り捨て" 警告が発行されます。 **StrLen_or_IndPtr**引数には、バッファーに格納されている文字数/バイト数が含まれます。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol による機能強化された日付と時刻のサポート  
 Date 型または time 型の結果列の値は、「 [SQL から C への変換](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)」で説明されているように変換されます。Time 列と datetimeoffset 列を対応する構造 (**SQL_SS_TIME2_STRUCT**および**SQL_SS_TIMESTAMPOFFSET_STRUCT**) として取得するには、 *TargetType*を**SQL_C_DEFAULT**または**SQL_C_BINARY**として指定する必要があることに注意してください。  
  
 詳細については、「[日付と&#40;時刻&#41;の機能強化 ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)」を参照してください。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol による大きな CLR UDT のサポート  
 **SQLBindCol**は、大きな CLR ユーザー定義型 (udt) をサポートしています。 詳細については、「 [LARGE CLR ユーザー定義&#40;型&#41;ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [SQLBindCol 関数](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 実装の詳細](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
