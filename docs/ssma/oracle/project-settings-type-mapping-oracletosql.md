---
title: プロジェクトの設定 (型のマッピング) (OracleToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4bb8466e-2199-4f00-8513-b04e9586723d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 4551181da22af1244f8083f6df5ea00f63e00e69
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266580"
---
# <a name="project-settings-type-mapping-oracletosql"></a>プロジェクトの設定 (型のマッピング) (OracleToSQL)
[型マッピング] ページ、**プロジェクト設定** ダイアログ ボックスには、SSMA に Oracle データ型に変換する方法をカスタマイズする設定が含まれています。[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型。  
  
型マッピング ページが表示されます、**プロジェクト設定**と**プロジェクト設定の既定の** ダイアログ ボックス。  
  
-   今後のすべての SSMA プロジェクトの設定を指定する、**ツール**ボタンをクリックし**プロジェクト設定の既定の**設定は表示またはから変更する必要な移行プロジェクトの種類を選択します **。移行ターゲット バージョン**ドロップダウンをクリックし、**型マッピングの**左側のウィンドウの下部にあります。  
  
-   現在のプロジェクトの設定を指定する、**ツール**ボタンをクリックし**プロジェクト設定**、順にクリックします**型マッピングの**左側のウィンドウの下部にあります。  
  
現在のオブジェクトまたはオブジェクトのクラスの設定を指定するには、使用、**型マッピングの**プライマリ SSMA ウィンドウでタブ。  
  
## <a name="options"></a>および  
次の表は、**型マッピングの**タブのオプション。  
  
**変換元の型**  
マップの Oracle データ型。  
  
**ターゲットの種類**  
ターゲット[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Oracle データ型のデータ型。  
  
SSMA for Oracle 型のマッピングの既定の次のセクションでテーブルを参照してください。  
  
**[追加]**  
データ型をマッピングの一覧に追加する をクリックします。  
  
**[編集]**  
マッピングの一覧で選択したデータ型を編集する をクリックします。  
  
**[削除]**  
マッピングの一覧から選択したデータ型のマッピングを削除する をクリックします。  
  
**既定値にリセット**  
SSMA の既定値に型マッピングのリストをリセットする をクリックします。  
  
## <a name="default-type-mappings"></a>既定の型マッピング  
SSMA for Oracle は、引数、列、ローカル変数、および戻り値のカスタム型マッピングを設定できます。 引数と戻り値の型の既定のマッピングとほぼ同じです。  
  
### <a name="default-argument-type-and-return-value-type-mapping"></a>既定の引数の型と値の型マッピングを返します  
次の表には、引数と戻り値の既定のデータ型マッピングが含まれています。  
  
|Oracle データ型|既定の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_integer|int|  
|blob (blob)|varbinary(max)|  
|boolean|bit|  
|char|varchar(max)|  
|char varying|varchar(max)|  
|character|varchar(max)|  
|character varying|varchar(max)|  
|Clob|varchar(max)|  
|日付|datetime2 [0]|  
|dec|dec [38] [0]|  
|Decimal|float [53]|  
|倍精度|float [53]|  
|FLOAT|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [\*..8000]<sup>*</sup>|varbinary [*]|  
|long raw [8001...\*]<sup>*</sup>|varbinary(max)|  
|national char|nvarchar(max)|  
|varying、national char|nvarchar(max)|  
|各国語文字|nvarchar(max)|  
|各国語文字 varying<sup>**</sup>|nvarchar(max)|  
|各国語文字 varying<sup>*</sup>|nvarchar(max)|  
|nchar|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|NUMERIC|float [53]|  
|nvarchar2|nvarchar(max)|  
|pls_integer|int|  
|raw|varbinary(max)|  
|REAL|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|signtype|SMALLINT|  
|SMALLINT|SMALLINT|  
|string|varchar(max)|  
|TIMESTAMP|datetime2|  
|ローカル タイム ゾーンのタイムスタンプ|datetimeoffset|  
|タイム ゾーンのタイムスタンプ|datetimeoffset|  
|urowid|UNIQUEIDENTIFIER|  
|varchar|varchar(max)|  
|varchar2|varchar(max)|  
|xmltype|xml|  
  
<sup>*</sup> 返す値の型マッピングのみに適用されます。  
  
<sup>**</sup> 引数の型マッピングのみに適用されます。  
  
### <a name="default-column-type-mapping"></a>既定の列の型マッピング  
次の表には、列の既定の型マッピングが含まれています。  
  
|Oracle データ型|既定の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|blob (blob)|varbinary(max)|  
|char|char|  
|char のさまざまな [*..\*]|varchar [*]|  
|char [*..\*]|char [*]|  
|character|char|  
|文字がさまざまな [*..\*]|varchar [*]|  
|文字 [*..\*]|char [*]|  
|Clob|varchar(max)|  
|日付|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*..\*]|dec [*] [0]|  
|dec [*..\*][\*..\*]|dec [*] [\*]|  
|Decimal|[38] [0] の 10 進数|  
|decimal [*..\*]|10 進数 [*] [0]|  
|decimal [*..\*][\*..\*]|10 進数 [*] [\*]|  
|倍精度|float [53]|  
|FLOAT|float [53]|  
|float [*..53]|float [*]|  
|float [54.. *]|float [53]|  
|int|int|  
|integer|int|  
|long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [*..8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|long varchar|varchar(max)|  
|長い [*..8000]|varchar [*]|  
|long[8001..*]|varchar(max)|  
|national char|nchar|  
|varying、national char [*..\*]|nvarchar [*]|  
|national char [*..\*]|nchar [*]|  
|各国語文字|nchar|  
|各国語文字がさまざまな [*..\*]|nvarchar [*]|  
|各国語文字 [*..\*]|nchar [*]|  
|nchar|nchar|  
|nchar [*]|nchar [*]|  
|Nclob|nvarchar(max)|  
|number|float [53]|  
|数 [*..\*]|数値 [*]|  
|数 [*..\*][\*..\*]|数値 [*] [\*]|  
|NUMERIC|NUMERIC|  
|数値 [*..\*]|数値 [*]|  
|数値 [*..\*][\*..\*]|数値 [*] [\*]|  
|nvarchar2[*..\*]|nvarchar [*]|  
|生 [*..\*]|varbinary [*]|  
|REAL|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|SMALLINT|SMALLINT|  
|TIMESTAMP|datetime2|  
|ローカル タイム ゾーンのタイムスタンプ|datetimeoffset|  
|ローカル タイム ゾーンのタイムスタンプ [*..\*]|datetimeoffset [*]|  
|タイム ゾーンのタイムスタンプ|datetimeoffset|  
|タイムスタンプとタイム ゾーン [*..\*]|datetimeoffset [*]|  
|タイムスタンプ [*..\*]|datetime2 [*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid [*..\*]|UNIQUEIDENTIFIER|  
|varchar [*..\*]|varchar [*]|  
|varchar2 [*..\*]|varchar [*]|  
|Xmltype|xml|  
  
### <a name="default-local-variable-type-mapping"></a>既定のローカル変数の型マッピング  
次の表には、ローカル変数の既定の型マッピングが含まれています。  
  
|Oracle データ型|既定の[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]データ型|  
|--------------------|-------------------------------------------------------------------------|  
|Bfile|varbinary(max)|  
|binary_double|float [53]|  
|binary_float|float [53]|  
|binary_interger|int|  
|Blob|varbinary(max)|  
|ブール値|bit|  
|Char|char|  
|char のさまざまな [*..8000]|varchar [*]|  
|char のさまざまな [8001.. *]|varchar(max)|  
|char [*..8000]|char [*]|  
|char [8001.. *]|varchar(max)|  
|文字|char|  
|文字がさまざまな [*..8000]|varchar [*]|  
|文字がさまざまな [8001.. *]|varchar(max)|  
|文字 [*..8000]|char [*]|  
|文字 [8001.. *]|varchar(max)|  
|Clob|varchar(max)|  
|日付|datetime2 [0]|  
|dec|dec [38] [0]|  
|dec [*..\*]|dec [*] [0]|  
|dec [*..\*][\*..\*]|dec [*] [\*]|  
|Decimal|[38] [0] の 10 進数|  
|decimal [*..\*]|10 進数 [*] [0]|  
|decimal [*..\*][\*..\*]|10 進数 [*] [\*]|  
|倍精度|float [53]|  
|Float|float [53]|  
|float [*..53]|float [*]|  
|float [54.. *]|float [53]|  
|Int|int|  
|整数型|int|  
|整数 [*..\*]|数値 [*] [0]|  
|Long|varchar(max)|  
|long raw|varbinary(max)|  
|long raw [*..8000]|varbinary [*]|  
|long raw [8001.. *]|varbinary(max)|  
|national char|nchar|  
|varying、national char [*..4000]|nvarchar [*]|  
|varying、national char [4001.. *]|nvarchar(max)|  
|national char [*..4000]|nchar [*]|  
|national char [4001.. *]|nvarchar(max)|  
|各国語文字|nchar|  
|各国語文字 [*..4000]|nvarchar [*]|  
|各国語文字 [4001.. *]|nvarchar(max)|  
|各国語文字がさまざまな [*..4000]|nvarchar [*]|  
|各国語文字がさまざまな [4001.. *]|nvarchar(max)|  
|Nchar|nchar|  
|nchar [*..4000]|nchar [*]|  
|nchar [4001.. *]|nvarchar(max)|  
|nchar のさまざまな [*..4000]|nvarchar [*]|  
|nchar のさまざまな [4001.. *]|nvarchar(max)|  
|Nclob|nvarchar(max)|  
|数値|float [53]|  
|数 [*..\*]|数値 [*]|  
|数 [*..\*][\*..\*]|数値 [*] [\*]|  
|数値|数値 [38] [0]|  
|数値 [*..\*]|数値 [*]|  
|数値 [*..\*][\*..\*]|数値 [*] [\*]|  
|nvarchar2 [*..4000]|nvarchar [*]|  
|nvarchar2 [4001.. *]|nvarchar(max)|  
|pls_integer|int|  
|生 [*..8000]|varbinary [*]|  
|生 [8001.. *]|varbinary(max)|  
|Real|float [53]|  
|Rowid|UNIQUEIDENTIFIER|  
|Signtype|SMALLINT|  
|Smallint|SMALLINT|  
|文字列 [*..8000]|varchar [*]|  
|文字列 [8001.. *]|varchar(max)|  
|TIMESTAMP|datetime2|  
|ローカル タイム ゾーンのタイムスタンプ|datetimeoffset|  
|タイム ゾーンのタイムスタンプ|datetimeoffset|  
|ローカル タイム ゾーンのタイムスタンプ [*..\*]|datetimeoffset [*]|  
|タイムスタンプとタイム ゾーン [*..\*]|datetimeoffset [*]|  
|タイムスタンプ [*..\*]|datetime2 [*]|  
|urowid|UNIQUEIDENTIFIER|  
|urowid [*..\*]|UNIQUEIDENTIFIER|  
|varchar [*..8000]|varchar [*]|  
|varchar [8001.. *]|varchar(max)|  
|varchar2 [*..8000]|varchar [*]|  
|varchar2 [8001.. *]|varcha(max)|  
|Xmltype|xml|  
  
## <a name="see-also"></a>関連項目  
[ユーザー インターフェイス リファレンス&#40;OracleToSQL&#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  
