---
title: プロジェクトの設定 (型のマッピング) (MySQLToSQL) |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 136fdf6d-657f-447b-af41-49bbc6e0e93e
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: beb82f2fd894af71bb6f291dcc6f86a995f8dd85
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138325"
---
# <a name="project-settings-type-mapping-mysqltosql"></a>プロジェクトの設定 (型のマッピング) (MySQLToSQL)
プロジェクトの型マッピングの設定では、SSMA プロジェクトの既定の型マッピングを設定できます。  

型のマッピングは、プロジェクトの設定とプロジェクトの既定の設定 ダイアログ ボックスで利用できます。  
  
-   プロジェクトの設定 ダイアログ ボックスを使用すると、現在のプロジェクトの構成オプションを設定できます。 型のマッピング設定の ツール メニューにアクセスするには、プロジェクトの設定 を選択し、左側のウィンドウで型のマッピングをクリックします。  
  
-   プロジェクトの既定の設定 ダイアログ ボックスを使用すると、すべてのプロジェクトの構成オプションを設定できます。 ツール メニューの設定を型のマッピングにアクセスするには、既定のプロジェクトの設定、移行プロジェクトの種類の設定は、表示/から変更する必要を選択します**移行ターゲット バージョン**ドロップダウンをクリックしての種類左側のウィンドウでマッピングします。  
  
## <a name="options"></a>および  
  
##### <a name="source-type"></a>[変換元の型]  
ターゲット データベースのデータ型にマップする必要がある MySQL のデータ型になります。  
  
##### <a name="target-type"></a>ターゲットの種類  
ターゲット データベースのデータは、指定の MySQL のデータ型の型します。  
  
##### <a name="add"></a>追加  
データ型をマッピングの一覧に追加する をクリックします。  
  
##### <a name="edit"></a>編集  
マッピングの一覧で選択したデータ型を編集する をクリックします。  
  
##### <a name="remove"></a>削除  
マッピングの一覧から選択したデータ型のマッピングを削除する をクリックします。  
  
##### <a name="reset-to-default"></a>[既定値にリセット]  
SSMA の既定値に型マッピングのリストをリセットする をクリックします。  
  
## <a name="type-mappings"></a>型のマッピング  
次の表は、ソースとターゲットのデータ型の既定のマッピングを示しています。  
  
|||  
|-|-|  
|**MySQL のデータ型**|**SQL Server データ型**|  
|BIGINT|BIGINT|  
|bigint [*..255]|BIGINT|  
|バイナリ|バイナリ [1]|  
|バイナリ [0..1]|バイナリ [1]|  
|バイナリ [2..255]|バイナリ [*]|  
|bit|バイナリ [1]|  
|ビット [0..8]|バイナリ [1]|  
|ビット [17..24]|バイナリ [3]|  
|ビット [25..32]|バイナリ [4]|  
|ビット [33..40]|バイナリ [5]|  
|ビット [41..48]|バイナリ [6]|  
|ビット [49..56]|バイナリ [7]|  
|ビット [57..64]|バイナリ [8]|  
|ビット [9..16]|バイナリ [2]|  
|blob (blob)|varbinary(max)|  
|blob [0..1]|varbinary [1]|  
|blob[2..8000]|varbinary [*]|  
|blob [8001.. *]|varbinary(max)|  
|bool|bit|  
|boolean|bit|  
|char|nchar [1]|  
|char バイト|バイナリ [1]|  
|バイト [0..1] char 型します。|バイナリ [1]|  
|バイト [2..255] char 型します。|バイナリ [*]|  
|char [0..1]|nchar [1]|  
|char [2..255]|nchar [*]|  
|character|nchar [1]|  
|文字のさまざまな [0..1]|nvarchar [1]|  
|文字のさまざまな [2..255]|NVARCHAR|  
|文字 [0..1]|nchar [1]|  
|文字 [2..255]|nchar [*]|  
|日付|日付|  
|DATETIME|datetime2 [0]|  
|dec|Decimal|  
|dec [*..65]|10 進数 [*] [0]|  
|dec [*..65] [\*..30]|10 進数 [*] [\*]|  
|Decimal|Decimal|  
|decimal [*..65]|10 進数 [*] [0]|  
|decimal [*..65] [\*..30]|10 進数 [*] [\*]|  
|double|float [53]|  
|倍精度|float [53]|  
|倍精度 [*..255] [\*..30]|数値 [*] [\*]|  
|二重 [*..255] [\*..30]|数値 [*] [\*]|  
|修正しました|NUMERIC|  
|固定 [*..65] [\*..30]|数値 [*] [\*]|  
|FLOAT|float [24]|  
|float [*..255] [\*..30]|数値 [*] [\*]|  
|float [*..53]|float [53]|  
|int|int|  
|int [*..255]|int|  
|integer|int|  
|整数 [*..255]|int|  
|longblob|varbinary(max)|  
|長いテキスト|nvarchar(max)|  
|mediumblob|varbinary(max)|  
|mediumint|int|  
|mediumint [*..255]|int|  
|mediumtext|nvarchar(max)|  
|national char|nchar [1]|  
|national char [0..1]|nchar [1]|  
|national char [2..255]|nchar [*]|  
|各国語文字|nchar [1]|  
|各国語文字がさまざまな|nvarchar [1]|  
|各国語文字の可変 [0..1]|nvarchar [1]|  
|各国語文字の可変 [2..4000]|nvarchar [*]|  
|各国語文字がさまざまな [4001.. *]|nvarchar(max)|  
|各国語文字 [0..1]|nchar [1]|  
|各国語文字 [2..255]|nchar [*]|  
|national varchar|nvarchar [1]|  
|national varchar [0..1]|nvarchar [1]|  
|national varchar [2..4000]|nvarchar [*]|  
|national varchar [4001.. *]|nvarchar(max)|  
|nchar|nchar [1]|  
|nchar varchar|nvarchar [1]|  
|nchar varchar [0..1]|nvarchar [1]|  
|nchar varchar [2..4000]|nvarchar [*]|  
|nchar varchar [4001.. *]|nvarchar(max)|  
|nchar [0..1]|nchar [1]|  
|nchar [2..255]|nchar [*]|  
|NUMERIC|NUMERIC|  
|数値 [*..65]|数値 [*] [0]|  
|数値 [*..65] [\*..30]|数値 [*] [\*]|  
|NVARCHAR|nvarchar [1]|  
|nvarchar [0..1]|nvarchar [1]|  
|nvarchar [2..4000]|nvarchar [*]|  
|nvarchar [4001.. *]|nvarchar(max)|  
|REAL|float [53]|  
|実際 [*..255] [\*..30]|数値 [*] [\*]|  
|シリアル|BIGINT|  
|SMALLINT|SMALLINT|  
|smallint [*..255]|SMALLINT|  
|text|nvarchar(max)|  
|テキスト [0..1]|nvarchar [1]|  
|text[2..4000]|nvarchar [*]|  
|テキスト [4001.. *]|nvarchar(max)|  
|time|time|  
|TIMESTAMP|DATETIME|  
|tinyblob|varbinary [255]|  
|TINYINT|SMALLINT|  
|tinyint [*..255]|SMALLINT|  
|tinytext|nvarchar [255]|  
|符号なし bigint|BIGINT|  
|符号なし bigint [*..255]|BIGINT|  
|符号なしの 12 月|Decimal|  
|符号なしの dec [*..65]|10 進数 [*] [0]|  
|符号なしの dec [*..65] [\*..30]|10 進数 [*] [\*]|  
|符号なし 10 進数|Decimal|  
|符号なし 10 進数 [*..65]|10 進数 [*] [0]|  
|符号なし 10 進数 [*..65] [\*..30]|10 進数 [*] [\*]|  
|倍精度浮動小数点符号なし|float [53]|  
|符号なしの倍精度|float [53]|  
|符号なしの倍精度 [*..255] [\*..30]|数値 [*] [\*]|  
|符号なしの倍精度浮動小数点 [*..255] [\*..30]|数値 [*] [\*]|  
|符号なしの固定|NUMERIC|  
|符号なしの固定 [*..65] [\*..30]|数値 [*] [\*]|  
|符号なしの float|float [24]|  
|符号なしの float [*..255] [\*..30]|数値 [*] [\*]|  
|符号なしの float [*..53]|float [53]|  
|unsigned int|BIGINT|  
|符号なし int [*..255]|BIGINT|  
|符号なし整数|BIGINT|  
|符号なし整数 [*..255]|BIGINT|  
|符号なしの mediumint|int|  
|符号なしの mediumint [*..255]|int|  
|unsigned numeric|NUMERIC|  
|符号なし数値 [*..65]|数値 [*] [0]|  
|符号なし数値 [*..65] [\*..30]|数値 [*] [\*]|  
|実際に符号なし|float [53]|  
|実際に署名されていない [*..255 [\*..30]|数値 [*] [\*]|  
|符号なしの smallint|int|  
|符号なしの smallint [*..255]|int|  
|符号なしの tinyint|TINYINT|  
|符号なしの tinyint [*..255]|TINYINT|  
|varbinary [0..1]|varbinary [1]|  
|varbinary [2..8000]|varbinary [*]|  
|varbinary [8001.. *]|varbinary(max)|  
|varchar [0..1]|nvarchar [1]|  
|varchar [2..4000]|nvarchar [*]|  
|varchar [4001.. *]|nvarchar(max)|  
|年|SMALLINT|  
|year [2..2]|SMALLINT|  
|year [4..4]|SMALLINT|  
  
##### <a name="add"></a>追加  
データ型をマッピングの一覧に追加する をクリックします。  
  
##### <a name="edit"></a>編集  
データ型マッピングのリストを編集する をクリックします。  
  
##### <a name="remove"></a>削除  
マッピングの一覧から選択したデータ型のマッピングを削除する をクリックします。  
  
##### <a name="reset-to-default"></a>[既定値にリセット]  
すべてのデータ型マッピングを SSMA の既定値にリセットする をクリックします。  
  
