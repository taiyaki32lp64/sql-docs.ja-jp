---
title: 格納 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- DataTypeEnum
helpviewer_keywords:
- DataTypeEnum enumeration [ADO]
ms.assetid: 2c57eca6-9336-4b06-ba10-9fef5926b1d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 27386894ce6d1d393505d49b4863a0ba9bf3320b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933221"
---
# <a name="datatypeenum"></a>DataTypeEnum
データ型を指定します、[フィールド](../../../ado/reference/ado-api/field-object.md)、[パラメーター](../../../ado/reference/ado-api/parameter-object.md)、または[プロパティ](../../../ado/reference/ado-api/property-object-ado.md)します。 次の表の説明 列では、かっこは、対応する OLE DB 型インジケーターに表示されます。  
  
|定数|Value|説明|  
|--------------|-----------|-----------------|  
|**AdArray**|0x2000|フラグの値は、常に別のデータ型定数は、その他のデータ型の配列を示すと組み合わせます。 ADOX には適用されません。|  
|**adBigInt**|20|8 バイト符号付き整数 (DBTYPE_I8) を示します。|  
|**adBinary**|128|バイナリ値 (DBTYPE_BYTES) を示します。|  
|**adBoolean**|11|示す、**ブール**値 (DBTYPE_BOOL)。|  
|**adBSTR**|8|Null で終わる文字の文字列 (Unicode) (DBTYPE_BSTR) を示します。|  
|**adChapter**|136|子の行セット (DBTYPE_HCHAPTER) 内の行を識別する 4 バイトの章の値を示します。|  
|**adChar**|129|文字列値 (DBTYPE_STR) を示します。|  
|**adCurrency**|6|通貨値 (DBTYPE_CY) を示します。 通貨は、小数点の右側には 4 桁の固定小数点数です。 これは、10,000 を掛け、8 バイト符号付き整数に格納されます。|  
|**adDate**|7|日付値 (DBTYPE_DATE) を示します。 日付は、整数部分は 1899 年 12 月 30 日からの日数の数と、小数部分は日の端数を double として格納されます。|  
|**adDBDate**|133|日付 (yyyymmdd) (DBTYPE_DBDATE) の値を示します。|  
|**adDBTime**|134|時刻値 (hhmmss) (DBTYPE_DBTIME) を示します。|  
|**adDBTimeStamp**|135|日付/時刻のスタンプ (yyyymmddhhmmss と 10億分数) を示します (DBTYPE_DBTIMESTAMP)。|  
|**adDecimal**|14|固定有効桁数と小数点 (DBTYPE_DECIMAL) が、正確な数値を示します。|  
|**adDouble**|5|倍精度浮動小数点値 (DBTYPE_R8) を示します。|  
|**adEmpty**|0|値 (DBTYPE_EMPTY) を指定しません。|  
|**adError**|10|32 ビット エラー コード (DBTYPE_ERROR) を示します。|  
|**adFileTime**|64|1601 年 1 月 1 日 (DBTYPE_FILETIME) から 100 ナノ秒間隔の数を表す 64 ビット値を示します。|  
|**adGUID**|72|グローバル一意識別子 (GUID) (DBTYPE_GUID) を示します。|  
|**adIDispatch**|9|ポインターを示します、 **IDispatch**インターフェイスを COM オブジェクト (DBTYPE_IDISPATCH)。<br /><br /> **注**ADO で現在はこのデータ型はできません。 使用量予測できない結果があります。|  
|**adInteger**|3|4 バイト符号付き整数 (DBTYPE_I4) を示します。|  
|**adIUnknown**|13|ポインターを示します、 **IUnknown**インターフェイスを COM オブジェクト (DBTYPE_IUNKNOWN)。<br /><br /> **注**ADO で現在はこのデータ型はできません。 使用量予測できない結果があります。|  
|**adLongVarBinary**|205|長のバイナリ値を示します。|  
|**adLongVarChar**|201|長い文字列値を示します。|  
|**adLongVarWChar**|203|時間の長い null で終わる Unicode 文字列値を示します。|  
|**adNumeric**|131|固定有効桁数と小数点 (DBTYPE_NUMERIC) が、正確な数値を示します。|  
|**adPropVariant**|138|オートメーション PROPVARIANT (DBTYPE_PROP_VARIANT) を示します。|  
|**adSingle**|4|単精度浮動小数点値 (DBTYPE_R4) を示します。|  
|**adSmallInt**|2|2 バイト符号付き整数 (DBTYPE_I2) を示します。|  
|**adTinyInt**|16|1 バイト符号付き整数 (DBTYPE_I1) を示します。|  
|**adUnsignedBigInt**|21|8 バイト符号なし整数 (DBTYPE_UI8) を示します。|  
|**adUnsignedInt**|19|4 バイト符号なし整数 (DBTYPE_UI4) を示します。|  
|**adUnsignedSmallInt**|18|2 バイト符号なし整数 (DBTYPE_UI2) を示します。|  
|**adUnsignedTinyInt**|17|1 バイト符号なし整数 (DBTYPE_UI1) を示します。|  
|**adUserDefined**|132|ユーザー定義変数 (DBTYPE_UDT) を示します。|  
|**adVarBinary**|204|バイナリ値を示します。|  
|**adVarChar**|200|文字列値を示します。|  
|**adVariant**|12|オートメーション オブジェクトを示す**バリアント**(DBTYPE_VARIANT)。<br /><br /> **注**ADO で現在はこのデータ型はできません。 使用量予測できない結果があります。|  
|**adVarNumeric**|139|数値の値を示します。|  
|**adVarWChar**|202|Null で終わる Unicode 文字列を示します。|  
|**adWChar**|130|Null で終わる Unicode 文字列 (DBTYPE_WSTR) を示します。|  
  
## <a name="adowfc-equivalent"></a>ADO と WFC と同等  
 パッケージ: **com.ms.wfc.data**  
  
|定数|  
|--------------|  
|AdoEnums.DataType.ARRAY|  
|AdoEnums.DataType.BIGINT|  
|AdoEnums.DataType.BINARY|  
|AdoEnums.DataType.BOOLEAN|  
|AdoEnums.DataType.BSTR|  
|AdoEnums.DataType.CHAPTER|  
|AdoEnums.DataType.CHAR|  
|AdoEnums.DataType.CURRENCY|  
|AdoEnums.DataType.DATE|  
|AdoEnums.DataType.DBDATE|  
|AdoEnums.DataType.DBTIME|  
|AdoEnums.DataType.DBTIMESTAMP|  
|AdoEnums.DataType.DECIMAL|  
|AdoEnums.DataType.DOUBLE|  
|AdoEnums.DataType.EMPTY|  
|AdoEnums.DataType.ERROR|  
|AdoEnums.DataType.FILETIME|  
|AdoEnums.DataType.GUID|  
|AdoEnums.DataType.IDISPATCH|  
|AdoEnums.DataType.INTEGER|  
|AdoEnums.DataType.IUNKNOWN|  
|AdoEnums.DataType.LONGVARBINARY|  
|AdoEnums.DataType.LONGVARCHAR|  
|AdoEnums.DataType.LONGVARWCHAR|  
|AdoEnums.DataType.NUMERIC|  
|AdoEnums.DataType.PROPVARIANT|  
|AdoEnums.DataType.SINGLE|  
|AdoEnums.DataType.SMALLINT|  
|AdoEnums.DataType.TINYINT|  
|AdoEnums.DataType.UNSIGNEDBIGINT|  
|AdoEnums.DataType.UNSIGNEDINT|  
|AdoEnums.DataType.UNSIGNEDSMALLINT|  
|AdoEnums.DataType.UNSIGNEDTINYINT|  
|AdoEnums.DataType.USERDEFINED|  
|AdoEnums.DataType.VARBINARY|  
|AdoEnums.DataType.VARCHAR|  
|AdoEnums.DataType.VARIANT|  
|AdoEnums.DataType.VARNUMERIC|  
|AdoEnums.DataType.VARWCHAR|  
|AdoEnums.DataType.WCHAR|  
  
## <a name="applies-to"></a>適用対象  
  
|||  
|-|-|  
|[Append メソッド (ADO)](../../../ado/reference/ado-api/append-method-ado.md)|[CreateParameter メソッド (ADO)](../../../ado/reference/ado-api/createparameter-method-ado.md)|  
|[CreateRecordset メソッド (RDS)](../../../ado/reference/rds-api/createrecordset-method-rds.md)|[Type プロパティ (ADO)](../../../ado/reference/ado-api/type-property-ado.md)|
