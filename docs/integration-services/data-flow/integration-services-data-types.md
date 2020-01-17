---
title: Integration Services のデータ型 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data types
- data types [Integration Services], listed
- data types [Integration Services]
- column data types [Integration Services]
- SSIS, data types
- Integration Services, data types
- SQL Server Integration Services, data types
ms.assetid: 896fc3e8-3aa6-4396-ba82-5d7741cffa56
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 45ada0520d90c1c6e63adad4f9e62bf1ea31e270
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292413"
---
# <a name="integration-services-data-types"></a>Integration Services のデータ型

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  データがパッケージ内のデータ フローに入ると、データを抽出する変換元は、そのデータを [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に変換します。 数値データは数値データ型、文字列データは文字列データ型、および日付データは日付データ型に割り当てられます。 GUID やバイナリ ラージ オブジェクト (BLOB) などの他のデータも、同様に適切な [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に割り当てられます。 データのデータ型が [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型に変換できない場合は、エラーが発生します。  
  
 一部のデータ フロー コンポーネントでは、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型と [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]のマネージド データ型の間でデータ型を変換します。 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] データ型とマネージド データ型とのマッピングの詳細については、「[データ フロー内のデータ型の処理](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)」を参照してください。  
  
 次の表に、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型を一覧で示します。 表内の一部のデータ型には、これらのデータ型に適用される有効桁数と小数点以下桁数の情報が含まれています。 有効桁数と小数点以下桁数の詳細については、「[有効桁数、小数点以下桁数、および長さ &#40;Transact-SQL&#41;](../../t-sql/data-types/precision-scale-and-length-transact-sql.md)」を参照してください。  
  
|データ型|[説明]|  
|---------------|-----------------|  
|DT_BOOL|ブール値です。|  
|DT_BYTES|バイナリ データ値です。 長さは可変で、最大長は 8,000 バイトです。|  
|DT_CY|通貨値です。 このデータ型は、8 バイトの符号付き整数で、4 の小数点以下桁数を持ち、最大有効桁数は 19 です。|  
|DT_DATE|年、月、日、時間、分、秒、および秒未満の時間で構成される日付の構造体です。  秒未満の固定された小数点以下桁数は 7 です。<br /><br /> DT_DATE データ型は、8 バイトの浮動小数点数を使用して実装されます。 年、月、日は、1899 年 12 月 30 日の午前 0 時を 0 とし、そこからの経過日数が整数で表されます。 時間の値は、数値の小数部分の絶対値で表されます。 ただし、浮動小数点数値ではすべての実数値を表すことができません。したがって、DT_DATE で表すことができる日付の範囲には制限があります。<br /><br /> 一方、DT_DBTIMESTAMP は、年、月、日、時間、分、秒、およびミリ秒の個別のフィールドを内部に持つ構造体で表されます。 このデータ型で表すことができる日付の範囲には緩い制限が課されています。|  
|DT_DBDATE|年、月、および日で構成される日付の構造体です。|  
|DT_DBTIME|時間、分、および秒で構成される時間の構造体です。|  
|DT_DBTIME2|時間、分、秒、および秒未満の時間で構成される時間の構造体です。 秒未満の最大小数点以下桁数は 7 です。|  
|DT_DBTIMESTAMP|年、月、日、時間、分、秒、および秒未満の時間で構成されるタイムスタンプの構造体です。 秒未満の最大小数点以下桁数は 3 です。|  
|DT_DBTIMESTAMP2|年、月、日、時間、分、秒、および秒未満の時間で構成されるタイムスタンプの構造体です。 秒未満の最大小数点以下桁数は 7 です。|  
|DT_DBTIMESTAMPOFFSET|年、月、日、時間、分、秒、および秒未満の時間で構成されるタイムスタンプの構造体です。 秒未満の最大小数点以下桁数は 7 です。<br /><br /> DT_DBTIMESTAMP および DT_DBTIMESTAMP2 のデータ型とは異なり、DT_DBTIMESTAMPOFFSET データ型にはタイム ゾーン オフセットがあります。 このオフセットには、協定世界時 (UTC) からのオフセット (時間および分) を指定します。 タイム ゾーン オフセットは、システムでローカル時間を取得するために使用されます。<br /><br /> タイム ゾーン オフセットには正符号または負符号を含めて、UTC を基準としてオフセットを加算するか、減算するかを示す必要があります。 時間の有効なオフセットは、-14 ～ +14 の範囲の値です。 分のオフセットの符号は、時間のオフセットの符号に依存します。<br /><br /> 時間のオフセットの符号が負である場合は、分のオフセットを負またはゼロにする必要があります。<br /><br /> 時間のオフセットの符号が正である場合は、分のオフセットを正またはゼロにする必要があります。<br /><br /> 時間のオフセットの符号がゼロである場合、分のオフセットには -0.59 ～ +0.59 の範囲の任意の値を指定できます。|  
|DT_DECIMAL|有効桁数と小数点以下桁数が固定長の、正確な数値です。 このデータ型は、12 バイトの符号なし整数で、区切り記号および 0 から 28 までの小数点以下桁数を持ち、最大有効桁数は 29 です。|  
|DT_FILETIME|1601 年 1 月 1 日以降を、100 ナノ秒間隔の数で表す 64 ビット値です。 秒未満の最大小数点以下桁数は 3 です。|  
|DT_GUID|グローバル一意識別子 (GUID) です。|  
|DT_I1|1 バイトの符号付き整数です。|  
|DT_I2|2 バイトの符号付き整数です。|  
|DT_I4|4 バイトの符号付き整数です。|  
|DT_I8|8 バイトの符号付き整数です。|  
|DT_NUMERIC|有効桁数と小数点以下桁数が固定長の、正確な数値です。 このデータ型は、16 バイトの符号なし整数で、区切り記号および 0 から 38 までの小数点以下桁数を持ち、最大有効桁数は 38 です。|  
|DT_R4|単精度浮動小数点値です。|  
|DT_R8|倍精度浮動小数点値です。|  
|DT_STR|NULL で終わる [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 文字の文字列で、最大長は 8,000 文字です。 列の値に追加の NULL ターミネータが含まれている場合、その文字列は最初に NULL が出現した箇所で切り捨てられます。|  
|DT_UI1|1 バイトの符号なし整数です。|  
|DT_UI2|2 バイトの符号なし整数です。|  
|DT_UI4|4 バイトの符号なし整数です。|  
|DT_UI8|8 バイトの符号なし整数です。|  
|DT_WSTR|NULL で終わる Unicode 文字の文字列で、最大長は 4,000 文字です。 列の値に追加の NULL ターミネータが含まれている場合、その文字列は最初に NULL が出現した箇所で切り捨てられます。|  
|DT_IMAGE|最大サイズが 2^31-1 (2,147,483,647) バイトのバイナリ値です。 のマネージ データ型の間でデータ型を変換します。|  
|DT_NTEXT|最大長が 2^30 - 1 (1,073,741,823) 文字の Unicode 文字列です。|  
|DT_TEXT|最大長が 2^31-1 (2,147,483,647) 文字の [!INCLUDE[vcpransi](../../includes/vcpransi-md.md)]/MBCS 文字列です。|  
  
## <a name="conversion-of-data-types"></a>データ型の変換  
 列のデータが、変換元のデータ型で割り当てられている長さや桁数をいっぱいまで使用する必要がない場合は、その列のデータ型を変更できます。 各データ行をできるだけ小さくすることにより、データ転送時のパフォーマンスを最適化できます。行が小さくなるほど、変換元から変換先へのデータ移動が高速になるためです。  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] には、数値データ型のセットすべてが含まれているので、データのサイズに最も近いデータ型を選択できます。 たとえば、DT_UI8 データ型の列の値が常に 0 から 3,000 までの整数の場合、このデータ型は DT_UI2 に変更できます。 同様に、DT_CY データ型の列が、整数データ型を使用するパッケージのデータ要件を満たしている場合は、データ型を DT_I4 に変更できます。  
  
 列のデータ型は、次の方法で変更できます。  
  
-   式を使用して、データ型を暗黙的に変換します。 詳細については、「[式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」、「[式における Integration Services データ型](../../integration-services/expressions/integration-services-data-types-in-expressions.md)」、「[Integration Services &#40;SSIS&#41; の式](../../integration-services/expressions/integration-services-ssis-expressions.md)」を参照してください。  
  
-   キャスト演算子を使用して、データ型を変換します。 詳細については、「[Cast &#40;SSIS 式&#41;](../../integration-services/expressions/cast-ssis-expression.md)」をご覧ください。  
  
-   データ変換の変換を使用して、列のデータ型を別のデータ型にキャストします。 詳細については、「 [Data Conversion Transformation](../../integration-services/data-flow/transformations/data-conversion-transformation.md)」を参照してください。  
  
-   派生列変換を使用して、元の列とは異なるデータ型を持つ列のコピーを作成します。 詳細については、「 [派生列変換](../../integration-services/data-flow/transformations/derived-column-transformation.md)」を参照してください。  
  
### <a name="converting-between-strings-and-datetime-data-types"></a>文字列と日付/時刻データ型間の変換  
 次の表に、日付/時刻データ型と文字列の間でキャストまたは変換を行った結果の一覧を示します。  
  
-   キャスト演算子またはデータ変換の変換を使用した場合、日付または時刻のデータ型は対応する文字列形式に変換されます。 たとえば、DT_DBTIME データ型は "hh:mm:ss" 形式の文字列に変換されます。  
  
-   文字列から日付または時刻のデータ型に変換する場合は、適切な日付または時刻のデータ型に対応した形式の文字列を使用する必要があります。 たとえば、日付の文字列を DT_DBDATE データ型に正常に変換するには、この日付の文字列は "yyyy-mm-dd" 形式である必要があります。  
  
    |データ型|文字列の形式|  
    |---------------|-------------------|  
    |DT_DBDATE|yyyy-mm-dd|  
    |DT_FILETIME|yyyy-mm-dd hh:mm:ss:fff|  
    |DT_DBTIME|hh:mm:ss|  
    |DT_DBTIME2|hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMP|yyyy-mm-dd hh:mm:ss[.fff]|  
    |DT_DBTIMESTAMP2|yyyy-mm-dd hh:mm:ss[.fffffff]|  
    |DT_DBTIMESTAMPOFFSET|yyyy-mm-dd hh:mm:ss[.fffffff] [{+&#124;-} hh:mm]|  
  
 DT_FILETIME および DT_DBTIMESTAMP の形式では、fff は秒の小数部を表す 0 ～ 999 の範囲の値になります。  
  
 DT_DBTIMESTAMP2、DT_DBTIME2、および DT_DBTIMESTAMPOFFSET の日付形式では、fffffff は秒の小数部を表す 0 ～ 9999999 の範囲の値になります。  
  
 DT_DBTIMESTAMPOFFSET の日付形式にはタイム ゾーン要素も含まれます。 時間要素とタイム ゾーン要素の間にはスペースがあります。  
  
### <a name="converting-datetime-data-types"></a>日付/時刻データ型の変換  
 日付または時刻のデータを含む列のデータ型を変更し、データの一部である日付または時刻を抽出できます。 次の表に、日付/時刻データ型を別の日付/時刻データ型に変換した結果を示します。  
  
#### <a name="converting-from-dt_filetime"></a>DT_FILETIME からの変換  
  
|DT_FILETIME の変換|結果|  
|-----------------------------|------------|  
|DT_FILETIME|変更なし。|  
|DT_DATE|データ型を変換します。|  
|DT_DBDATE|時刻値を削除します。|  
|DT_DBTIME|日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME データ型に含めることのできる小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIME2|DT_FILETIME データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP|データ型を変換します。|  
|DT_DBTIMESTAMP2|秒の小数点以下桁数が、DT_DBTIMESTAMP2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型のタイム ゾーン フィールドをゼロに設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMPOFFSET データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
  
#### <a name="converting-from-dt_date"></a>DT_DATE からの変換  
  
|DT_DATE の変換|結果|  
|-------------------------|------------|  
|DT_FILETIME|データ型を変換します。|  
|DT_DATE|変更なし。|  
|DT_DBDATE|DT_DATA データ型で表される時刻値を削除します。|  
|DT_DBTIME|DT_DATE データ型で表される日付値を削除します。|  
|DT_DBTIME2|DT_DATE データ型で表される日付値を削除します。|  
|DT_DBTIMESTAMP|データ型を変換します。|  
|DT_DBTIMESTAMP2|データ型を変換します。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型のタイム ゾーン フィールドをゼロに設定します。|  
  
#### <a name="converting-from-dt_dbdate"></a>DT_DBDATE からの変換  
  
|DT_DBDATE の変換|結果|  
|---------------------------|------------|  
|DT_FILETIME|DT_FILETIME データ型の時刻フィールドをゼロに設定します。|  
|DT_DATE|DT_DATE データ型の時刻フィールドをゼロに設定します。|  
|DT_DBDATE|変更なし。|  
|DT_DBTIME|DT_DBTIME データ型の時刻フィールドをゼロに設定します。|  
|DT_DBTIME2|DT_DBTIME2 データ型の時刻フィールドをゼロに設定します。|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP データ型の時刻フィールドをゼロに設定します。|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP データ型の時刻フィールドをゼロに設定します。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型の時刻フィールドとタイム ゾーン フィールドをゼロに設定します。|  
  
#### <a name="converting-from-dt_dbtime"></a>DT_DBTIME からの変換  
  
|DT_DBTIME の変換|結果|  
|---------------------------|------------|  
|DT_FILETIME|DT_FILETIME データ型の日付フィールドを現在の日付に設定します。|  
|DT_DATE|DT_DATE データ型の日付フィールドを現在の日付に設定します。|  
|DT_DBDATE|DT_DBDATE データ型の日付フィールドを現在の日付に設定します。|  
|DT_DBTIME|変更なし。|  
|DT_DBTIME2|データ型を変換します。|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP データ型の日付フィールドを現在の日付に設定します。|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP2 データ型の日付フィールドを現在の日付に設定します。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型の日付フィールドとタイム ゾーン フィールドをそれぞれ現在の日付とゼロに設定します。|  
  
#### <a name="converting-from-dt_dbtime2"></a>DT_DBTIME2 からの変換  
  
|DT_DBTIME2 の変換|結果|  
|----------------------------|------------|  
|DT_FILETIME|DT_FILETIME データ型の日付フィールドを現在の日付に設定します。<br /><br /> 秒の小数点以下桁数が、DT_FILETIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DATE|DT_DATE データ型の日付フィールドを現在の日付に設定します。<br /><br /> 秒の小数点以下桁数が、DT_DATE データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBDATE|DT_DBDATE データ型の日付フィールドを現在の日付に設定します。|  
|DT_DBTIME|秒の小数点以下桁数が、DT_DBTIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIME2|秒の小数点以下桁数が、変換先の DT_DBTIME2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP データ型の日付フィールドを現在の日付に設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMP データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMP2 データ型の日付フィールドを現在の日付に設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMP2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型の日付フィールドとタイム ゾーン フィールドをそれぞれ現在の日付とゼロに設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMPOFFSET データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
  
#### <a name="converting-from-dt_dbtimestamp"></a>DT_DBTIMESTAMP からの変換  
  
|DT_DBTIMESTAMP の変換|結果|  
|--------------------------------|------------|  
|DT_FILETIME|データ型を変換します。|  
|DT_DATE|DT_DBTIMESTAMP データ型によって表される値が DT_DATE データ型の範囲からオーバーフローする場合は、DB_E_DATAOVERFLOW エラーを返します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBDATE|DT_DBTIMESTAMP データ型で表される時刻値を削除します。|  
|DT_DBTIME|DT_DBTIMESTAMP データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIME2|DT_DBTIMESTAMP データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP|変更なし。|  
|DT_DBTIMESTAMP2|秒の小数点以下桁数が、DT_DBTIMESTAMP2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型のタイム ゾーン フィールドをゼロに設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMPOFFSET データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
  
#### <a name="converting-from-dt_dbtimestamp2"></a>DT_DBTIMESTAMP2 からの変換  
  
|DT_DBTIMESTAMP2 の変換|結果|  
|---------------------------------|------------|  
|DT_FILETIME|秒の小数点以下桁数が、DT_FILETIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DATE|DT_DBTIMESTAMP2 データ型によって表される値が DT_DATE データ型の範囲からオーバーフローする場合は、DB_E_DATAOVERFLOW エラーが返されます。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。<br /><br /> 秒の小数点以下桁数が、DT_DATE データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBDATE|DT_DBTIMESTAMP2 データ型で表される時刻値を削除します。|  
|DT_DBTIME|DT_DBTIMESTAMP2 データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIME2|DT_DBTIMESTAMP2 データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMP2 データ型によって表される値が DT_DBTIMESTAMP データ型の範囲からオーバーフローする場合は、DB_E_DATAOVERFLOW エラーを返します。<br /><br /> DT_DBTIMESTAMP2 は、西暦 1 年 1 月 1 日～ 9999 年 12 月 31 日の範囲の SQL Server データ型、 datetime2 にマップされます。 DT_DBTIMESTAMP は、1753 年 1 月 1 日～ 9999 年 12 月 31 日のより小さな範囲の SQL Server データ型、datetime にマップされます。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMP データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。<br /><br /> エラーの詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP2|秒の小数点以下桁数が、変換先の DT_DBTIMESTAMP2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMPOFFSET|DT_DBTIMESTAMPOFFSET データ型のタイム ゾーン フィールドをゼロに設定します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMPOFFSET データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
  
#### <a name="converting-from-dt_dbtimestampoffset"></a>DT_DBTIMESTAMPOFFSET からの変換  
  
|DT_DBTIMESTAMPOFFSET の変換|結果|  
|--------------------------------------|------------|  
|DT_FILETIME|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を協定世界時 (UTC) に変更します。<br /><br /> 秒の小数点以下桁数が、DT_FILETIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DATE|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を UTC に変更します。<br /><br /> DT_DBTIMESTAMPOFFSET データ型によって表される値が DT_DATE データ型の範囲からオーバーフローする場合は、DB_E_DATAOVERFLOW エラーを返します。<br /><br /> 秒の小数点以下桁数が、DT_DATE データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。<br /><br /> 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBDATE|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を、日付値に影響を及ぼす可能性のある UTC に変更します。 時刻値が次に削除されます。|  
|DT_DBTIME|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を UTC に変更します。<br /><br /> DT_DBTIMESTAMPOFFSET データ型で表されるデータ値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIME2|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を UTC に変更します。<br /><br /> DT_DBTIMESTAMPOFFSET データ型で表される日付値を削除します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIME2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を UTC に変更します。<br /><br /> DT_DBTIMESTAMPOFFSET データ型によって表される値が DT_DBTIMESTAMP データ型の範囲からオーバーフローする場合は、DB_E_DATAOVERFLOW エラーが返されます。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMP データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。<br /><br /> 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMP2|DT_DBTIMESTAMPOFFSET データ型で表される時刻値を UTC に変更します。<br /><br /> 秒の小数点以下桁数が、DT_DBTIMESTAMP2 データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
|DT_DBTIMESTAMPOFFSET|秒の小数点以下桁数が、変換先の DT_DBTIMESTAMPOFFSET データ型に含めることのできる秒の小数点以下桁数よりも大きい場合に、秒の小数部の値を削除します。 秒の小数部の値を削除した後、このデータの切り捨てに関するレポートを生成します。 詳細については、「 [データのエラー処理](../../integration-services/data-flow/error-handling-in-data.md)」を参照してください。|  
  
## <a name="mapping-of-integration-services-data-types-to-database-data-types"></a>Integration Services のデータ型とデータベースのデータ型とのマッピング  
 次の表に、特定のデータベースによって使用されるデータ型を [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] のデータ型にマッピングする際のガイダンスを示します。 これらのマッピングは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インポートおよびエクスポート ウィザードでソースからデータをインポートする際に使用されるマッピング ファイルから集約されます。 これらのマッピング ファイルの詳細については、「 [SQL Server インポートおよびエクスポート ウィザード](~/integration-services/import-export-data/welcome-to-sql-server-import-and-export-wizard.md)」を参照してください。  
  
> [!IMPORTANT]  
>  これらのマッピングは厳密な対応関係を表しているわけではなく、ガイダンスの提供のみを目的としています。 場合によっては、この表に示されているデータ型とは異なるデータ型を使用する必要があります。  
  
> [!NOTE]  
>  対応する Integration Services の日付と時刻のデータ型のサイズを推定するために、SQL Server データ型を使用できます。  
  
|データ型|SQL Server<br /><br /> (SQLOLEDB、SQLNCLI10)|SQL Server (SqlClient)|Jet|Oracle<br /><br /> (OracleClient)|DB2<br /><br /> (DB2OLEDB)|DB2<br /><br /> (IBMDADB2)|  
|---------------|--------------------------------------------|------------------------------|---------|---------------------------------|--------------------------|--------------------------|  
|DT_BOOL|bit|bit|bit||||  
|DT_BYTES|binary、varbinary、timestamp|binary、varbinary、timestamp|BigBinary、VarBinary|RAW|||  
|DT_CY|smallmoney、money|smallmoney、money|Currency||||  
|DT_DATE|||||||  
|DT_DBDATE|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)|[date &#40;Transact-SQL&#41;](../../t-sql/data-types/date-transact-sql.md)||date|date|date|  
|DT_DBTIME||||TIMESTAMP|time|time|  
|DT_DBTIME2|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md)(p)|[time &#40;Transact-SQL&#41;](../../t-sql/data-types/time-transact-sql.md) (p)|||||  
|DT_DBTIMESTAMP|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)、[smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|[datetime &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime-transact-sql.md)、[smalldatetime &#40;Transact-SQL&#41;](../../t-sql/data-types/smalldatetime-transact-sql.md)|DateTime|TIMESTAMP、DATE、INTERVAL|TIME、TIMESTAMP、DATE|TIME、TIMESTAMP、DATE|  
|DT_DBTIMESTAMP2|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)|[datetime2 &#40;Transact-SQL&#41;](../../t-sql/data-types/datetime2-transact-sql.md)||TIMESTAMP|TIMESTAMP|TIMESTAMP|  
|DT_DBTIMESTAMPOFFSET|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md)(p)|[datetimeoffset &#40;Transact-SQL&#41;](../../t-sql/data-types/datetimeoffset-transact-sql.md) (p)||timestampoffset|timestamp、<br /><br /> varchar|timestamp、<br /><br /> varchar|  
|DT_DECIMAL|||||||  
|DT_FILETIME|||||||  
|DT_GUID|UNIQUEIDENTIFIER|UNIQUEIDENTIFIER|GUID||||  
|DT_I1|||||||  
|DT_I2|SMALLINT|SMALLINT|Short||smallint|SMALLINT|  
|DT_I4|INT|INT|Long||INTEGER|INTEGER|  
|DT_I8|BIGINT|BIGINT|||bigint|bigint|  
|DT_NUMERIC|decimal、numeric|decimal、numeric|Decimal|NUMBER、INT|decimal、numeric|decimal、numeric|  
|DT_R4|REAL|REAL|Single||real|real|  
|DT_R8|FLOAT|FLOAT|Double|FLOAT、REAL|FLOAT、DOUBLE|FLOAT、DOUBLE|  
|DT_STR|char、varchar||varchar||char、varchar|char、varchar|  
|DT_UI1|TINYINT|TINYINT|Byte||||  
|DT_UI2|||||||  
|DT_UI4|||||||  
|DT_UI8|||||||  
|DT_WSTR|nchar、nvarchar、sql_variant、xml|char、varchar、nchar、nvarchar、sql_variant、xml|LongText|CHAR、ROWID、VARCHAR2、NVARCHAR2、NCHAR|GRAPHIC、VARGRAPHIC|GRAPHIC、VARGRAPHIC|  
|DT_IMAGE|image|image|LongBinary|LONG RAW、BLOB、LOBLOCATOR、BFILE、VARGRAPHIC、LONG VARGRAPHIC、ユーザー定義型|CHAR () FOR BIT DATA、VARCHAR () FOR BIT DATA|CHAR () FOR BIT DATA、VARCHAR () FOR BIT DATA、BLOB|  
|DT_NTEXT|ntext|text、ntext||LONG、CLOB、NCLOB、NVARCHAR、TEXT|LONG VARCHAR、NCHAR、NVARCHAR、TEXT|LONG VARCHAR、DBCLOB、NCHAR、NVARCHAR、TEXT|  
|DT_TEXT|text||||LONG VARCHAR FOR BIT DATA|LONG VARCHAR FOR BIT DATA、CLOB|  
  
 データ フローでのデータのマッピングついては、「 [データ フロー内のデータ型の処理](../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)」を参照してください。  
  
## <a name="related-content"></a>関連コンテンツ  
 blogs.msdn.com のブログ「 [SSIS 2008 のデータ型の変換手法間のパフォーマンス比較](https://go.microsoft.com/fwlink/?LinkId=220823)」  
  
## <a name="see-also"></a>参照  
 [データ フロー内のデータ](../../integration-services/data-flow/data-in-data-flows.md)  
  
  
