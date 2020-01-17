---
title: 強化された日付と時刻型 (OLE DB および ODBC) の一括コピーの変更 |マイクロソフトのドキュメント
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, bulk copy operations
- bulk copy [ODBC], changes for date/time improvements
ms.assetid: c29e0f5e-9b3c-42b3-9856-755f4510832f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 855d0baf0b0b890b9343378f8060919979d5f206
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63207107"
---
# <a name="bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc"></a>機能強化された日付型と時刻型向けの一括コピーの変更 (OLE DB および ODBC)
  このトピックでは、一括コピー機能をサポートするための日付と時刻の機能強化について説明します。 このトピックの情報は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client の OLE DB と ODBC の両方に当てはまります。  
  
## <a name="format-files"></a>フォーマット ファイル  
 フォーマット ファイルを対話形式で作成する場合に、日付型と時刻型の指定に使用する入力、および対応するホスト ファイル データ型名を次の表に示します。  
  
|ファイル ストレージ型|ホスト ファイル データ型|プロンプトに応答します。"フィールド < field_name > のファイル ストレージ型を入力します [\<既定 >]:"。|  
|-----------------------|-------------------------|-----------------------------------------------------------------------------------------------------|  
|DATETIME|SQLDATETIME|d|  
|Smalldatetime|SQLDATETIM4|D|  
|date|SQLDATE|de|  
|Time|SQLTIME|te|  
|Datetime2|SQLDATETIME2|d2|  
|Datetimeoffset|SQLDATETIMEOFFSET|do|  
  
 XML フォーマット ファイルの XSD への追加内容を次に示します。  
  
```  
<xs:complexType name="SQLDATETIME2">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATETIMEOFFSET">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLDATE">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
<xs:complexType name="SQLTIME">  
    <xs:complexContent>  
        <xs:extension base="bl:Fixed"/>  
    </xs:complexContent>  
</xs:complexType>  
```  
  
## <a name="character-data-files"></a>文字データ ファイル  
 」の説明に従って文字のデータ ファイルで日付と時刻の値が表される、"データ形式。文字列とリテラル」のセクション[ODBC の日付と時刻の強化に対するデータ型のサポート](data-type-support-for-odbc-date-and-time-improvements.md)for ODBC、またはの[OLE DB の日付と時刻の強化に対するデータ型のサポート](../native-client-ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)OLE DB 用です。  
  
 桁数が 7 の TDS 表現としてのネイティブ データ ファイルでは、4 つの新しい型の日付と時刻の値が表されます (これは、最大でサポートされているため、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]と bcp データ ファイルは、これらの列の小数点以下桁数を格納しないでください)。 既存のストレージに変更がない`datetime`と`smalldatetime`型または表形式データ ストリーム (TDS) の表現。  
  
 OLE DB の場合、さまざまなストレージ型のストレージ サイズは次のとおりです。  
  
|ファイル ストレージ型|ストレージ サイズ (バイト単位)|  
|-----------------------|---------------------------|  
|DATETIME|8|  
|smalldatetime|4|  
|日付|3|  
|time|6|  
|datetime2|9|  
|datetimeoffset|11|  
  
 ODBC の場合、サイズは次のとおりです。 BCP.exe を実行すると有効桁数は常にサーバーから取得されるので、フォーマット ファイルにもデータ ファイルにも、有効桁数を格納する必要はありません。  
  
|ファイル ストレージ型|ストレージ サイズ (バイト単位)|ストレージ形式|  
|-----------------------|---------------------------|--------------------|  
|datetime (d)|8|TDS (TDS)|  
|smalldatetime (D)|4|TDS (TDS)|  
|date (de)|3|TDS (TDS)|  
|time (te)|6|TDS (TDS)|  
|datetime2 (d2)|9|TDS (TDS)|  
|datetimeoffset (do)|11|TDS (TDS)|  
  
## <a name="bcp-types-in-sqlnclih"></a>sqlncli.h 内の BCP 型  
 sqlncli.h では、ODBC の BCP API 拡張機能で使用する次の型が定義されています。 これらの型が渡され、 *eUserDataType* ibcpsession::bcpcolfmt OLE DB でのパラメーター。  
  
|ファイル ストレージ型|ホスト ファイル データ型|Ibcpsession::bcpcolfmt で使用するための sqlncli.h 内の型します。|値|  
|-----------------------|-------------------------|-----------------------------------------------------------|-----------|  
|DATETIME|SQLDATETIME|BCP_TYPE_SQLDATETIME|0x3d|  
|Smalldatetime|SQLDATETIM4|BCP_TYPE_SQLDATETIME4|0x3a|  
|date|SQLDATE|BCP_TYPE_SQLDATE|0x28|  
|Time|SQLTIME|BCP_TYPE_SQLTIME|0x29|  
|Datetime2|SQLDATETIME2|BCP_TYPE_SQLDATETIME2|0x2a|  
|Datetimeoffset|SQLDATETIMEOFFSET|BCP_TYPE_SQLDATETIMEOFFSET|0x2b|  
  
## <a name="bcp-data-type-conversions"></a>BCP データ型変換  
 次の表に、変換情報を示します。  
  
 **OLE DB に関するメモ** 次の変換は、IBCPSession によって実行されます。 IRowsetFastLoad で定義されている OLE DB 変換を使用して[サーバーにクライアントから変換](../native-client-ole-db-date-time/conversions-performed-from-client-to-server.md)します。 次に示すクライアントでの変換が実行されると、datetime 値は 1/300 秒単位に丸められ、smalldatetime 値の秒は 0 に設定されます。 datetime の丸め処理は、時間と分に適用されますが、日付には適用されません。  
  
|--> を<br /><br /> From|日付|time|smalldatetime|DATETIME|datetime2|datetimeoffset|char|wchar|  
|------------------------|----------|----------|-------------------|--------------|---------------|--------------------|----------|-----------|  
|date|1|-|1,6|1,6|1,6|1,5,6|1,3|1,3|  
|Time|なし|1,10|1,7,10|1,7,10|1,7,10|1,5,7,10|1,3|1,3|  
|Smalldatetime|1,2|1,4,10|1|1|1,10|1,5,10|1,11|1,11|  
|DATETIME|1,2|1,4,10|1,12|1|1,10|1,5,10|1,11|1,11|  
|Datetime2|1,2|1,4,10|1、10 (ODBC) 1、12 (OLE DB)|1,10|1,10|1,5,10|1,3|1,3|  
|Datetimeoffset|1,2,8|1,4,8,10|1,8,10|1,8,10|1,8,10|1,10|1,3|1,3|  
|Char/wchar (date)|9|-|9、6 (ODBC) 9、6、12 (OLE DB)|9、6 (ODBC) 9、6、12 (OLE DB)|9,6|9,5,6|なし|なし|  
|Char/wchar (time)|-|9,10|9、7、10 (ODBC) 9,7,10,12 (OLE DB)|9、7、10 (ODBC) 9、7、10、12 (OLE DB)|9,7,10|9,5,7,10|なし|なし|  
|Char/wchar (datetime)|9,2|9,4,10|9、10 (ODBC) 9、10、12 (OLE DB)|9、10 (ODBC) 9、10、12 (OLE DB)|9,10|9,5,10|なし|なし|  
|Char/wchar (datetimeoffset)|9,2,8|9,4,8,10|9、8、10 (ODBC) 9、8、10、12 (OLE DB)|9、8、10 (ODBC) 9、8、10、12 (OLE DB)|9,8,10|9,10|なし|なし|  
  
#### <a name="key-to-symbols"></a>記号の説明  
  
|シンボル|説明|  
|------------|-------------|  
|-|変換はサポートされていません。<br /><br /> "データ型の属性に関する制限に違反しました" というメッセージで SQLSTATE 07006 の ODBC 診断レコードが生成されます。|  
|1|指定したデータが無効な場合、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の ODBC 診断レコードが生成されます。 datetimeoffset 値の場合は、UTC への変換が必要なくても、時刻部分は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するためです。 したがって、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があります。|  
|2|時刻部分は無視されます。|  
|3|ODBC 用データの損失を伴う切り捨てが発生した場合、診断レコードが生成 SQLSTATE 22001、メッセージ '文字列データの右側が切り捨てられました' に従って変換先列のサイズから秒の小数部桁数 (スケール) の数が決まりますが、次の表にします。 テーブルの範囲よりサイズが大きい列の場合、7 桁と見なされます。 この変換は、9 秒の小数、ODBC で許容される最大まで許容されます。<br /><br /> **種類:** DBTIME2<br /><br /> **暗黙の小数点以下桁数 0** 8<br /><br /> **暗黙のスケール 1..7** 10,16<br /><br /> <br /><br /> **種類:** DBTIMESTAMP<br /><br /> **0 の暗黙的なスケール:** 19<br /><br /> **暗黙的なスケール 1..7:** 21..27<br /><br /> <br /><br /> **種類:** DBTIMESTAMPOFFSET<br /><br /> **0 の暗黙的なスケール:** 26<br /><br /> **暗黙的なスケール 1..7:** 28..34<br /><br /> OLE DB の場合は、データの損失を伴う切り捨てが行われると、エラーが通知されます。 datetime2 に関しては、次の表に示すように、秒の小数点以下桁数 (スケール) は変換先の列のサイズによって決まります。 テーブルの範囲よりサイズが大きい列の場合は、9 桁と見なされます。 この変換では、秒の小数点以下桁数が 9 桁まで許容されます。これは、OLE DB で許容される最大桁数です。<br /><br /> **種類:** DBTIME2<br /><br /> **暗黙の小数点以下桁数 0** 8<br /><br /> **暗黙の小数点以下桁数 1..9** 1..9<br /><br /> <br /><br /> **種類:** DBTIMESTAMP<br /><br /> **0 の暗黙的なスケール:** 19<br /><br /> **暗黙的なスケール 1..9:** 21..29<br /><br /> <br /><br /> **種類:** DBTIMESTAMPOFFSET<br /><br /> **0 の暗黙的なスケール:** 26<br /><br /> **暗黙的なスケール 1..9:** 28..36|  
|4|日付部分は無視されます。|  
|5|タイム ゾーンは UTC (00:00 など) に設定されます。|  
|6|時刻は 0 に設定されます。|  
|7|日付は 1900-01-01 に設定されます。|  
|8|タイム ゾーン オフセットは無視されます。|  
|9|文字列は解析され、最初に検出された句読点、および残りの部分があるかどうかに応じて、date 値、datetime 値、datetimeoffset 値、time 値のいずれかに変換されます。 次に、このトピックの最後にある表に示した規則のうち、この処理で検出された変換元の型についての規則に従って、文字列は変換先の型に変換されます。 指定したデータを解析するとエラーが発生する場合、データを構成するいずれかの部分が許容範囲の外にある場合、または、リテラル型から変換先の型への変換が存在しない場合は、エラーが通知される (OLE DB) か、"キャストした文字コードが正しくありません" というメッセージで SQLSTATE 22018 の ODBC 診断レコードが生成されます。 datetime 型および smalldatetime 型のパラメーターでは、年がこれらの型でサポートされる範囲外の場合、エラーが通知される (OLE DB) か、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の ODBC 診断レコードが生成されます。<br /><br /> datetimeoffset では、UTC への変換が必要なくても、値は UTC への変換後の範囲内に収まっている必要があります。 TDS とサーバーは datetimeoffset 値の時刻を常に UTC 用に正規化するので、クライアントは、時刻部分が、UTC への変換後にサポートされる範囲内に収まっていることを確認する必要があるためです。 値が、サポートされている UTC の範囲内にない場合、エラーが通知される (OLE DB) か、"datetime 形式が無効です" というメッセージで SQLSTATE 22007 の ODBC 診断レコードが生成されます。|  
|10|クライアントからサーバーへの変換で、データの損失を伴う切り捨てが行われると、エラーが通知される (OLE DB) か、"Datetime フィールド オーバーフロー" というメッセージで SQLSTATE 22008 の ODBC 診断レコードが生成されます。 サーバーが使用する UTC の範囲で表すことができる範囲の外に値がある場合にも、このエラーが発生します。 サーバーからクライアントへの変換で、秒または秒の小数部の切り捨てが行われた場合は、警告のみが発生します。|  
|11|データの損失を伴う切り捨てが行われると、診断レコードが生成されます。<br /><br /> サーバーからクライアントへの変換では、これは警告 (ODBC SQLSTATE S1000) です。<br /><br /> クライアントからサーバーへの変換では、これはエラー (ODBC SQLSTATE 22001) です。|  
|12|秒は 0 に設定され、秒の小数部は破棄されます。 切り捨てエラーは発生しません。|  
|なし|既存の [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 以前のバージョンの動作が維持されます。|  
  
## <a name="see-also"></a>参照  
 [日付と時刻の強化&#40;ODBC&#41;](date-and-time-improvements-odbc.md)   
 [日付と時刻の強化機能 &#40;OLE DB&#41;](../native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
