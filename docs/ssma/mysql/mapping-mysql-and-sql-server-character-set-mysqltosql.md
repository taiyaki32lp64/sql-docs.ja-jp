---
title: MySQL と SQL Server の文字のマッピング (MySQLToSQL) を設定 |Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 20b3f22e-16a2-4a87-b4eb-c277be6bf5c8
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 32d5e23579b99b323da870d2608b2d197520f99f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909020"
---
# <a name="mapping-mysql-and-sql-server-character-set-mysqltosql"></a>MySQL と SQL Server 文字セットのマッピング (MySQLToSQL)
MySQL の文字データ型、式とリテラルの文字セット (文字セット) を指定できます。  
  
## <a name="charset-mapping"></a>文字セットのマッピング  
文字セットのマッピングが各 MySQL 文字セットに対して定義されているし、文字データ型の変換中に使用します。 これには、特定の文字セットの文字の文字列データ型に変換する方法を指定します。  
  
-   国内の SQL Server 文字型 (NCHAR または NVARCHAR) するか、  
  
-   SQL Server に通常の文字型 (CHAR または VARCHAR)  
  
1.  **national**ターゲット データベースの文字データ型は。  
  
    1.  **nchar**  
  
    2.  **nvarchar**  
  
2.  **通常**ターゲット データベースの文字データ型は。  
  
    1.  **char**  
  
    2.  **varchar**  
  
3.  型のマッピングへのマッピングのみが許可**national**文字データ型。 型マッピングに従って MySQL 文字データ型を変換すると、文字セットのマッピングが適用されます。  
  
> [!NOTE]  
> 文字セットのマッピングでは、メタデータ オブジェクト エクスプ ローラーの各ノードのレベルで定義することができます、MySQL から読み取るすべての文字セットを表します。  
  
## <a name="charset-mapping-on-different-node-levels"></a>別のノードのレベルで文字セットのマッピング  
文字セットのマッピングによって異なります、別のノードのレベルに namely:  
  
1.  メタデータ ノードのルート レベルで  
  
2.  データベース、カテゴリ、およびオブジェクト ノードのレベル  
  
> [!NOTE]  
> 文字セットのマッピングを編集用に選択するタブには、別のノード レベルでのマッピングに関係なく、3 つのボタンが含まれています。  
>   
> これらは次のとおりです。  
>   
> 1.  **適用されます。** 文字セットのマッピングの編集し、保存されていない場合にのみ有効になっている、ユーザーが行った変更を適用します。  
> 2.  **キャンセル：** ユーザーによって行われた変更を取り消します。 文字セットのマッピングの編集が保存されない場合に、ボタンが有効に取得します。  
> 3.  **既定値にリセットします。** すべてのマッピングを既定値にリセットします。  
  
1.  **ルート ノードのメタデータ レベル。** 文字セットのマッピング グリッドには、列は、各文字のセットを別の文字セットのグリッドが含まれています。 グリッドの列は次のとおりです。  
  
    1.  という名前のグリッドの最初の列**文字セット名**文字セットの名前が含まれています。  
  
    2.  という名前の 2 つ目**Charset 説明**文字セットの説明が含まれています。  
  
    3.  3 番目の列のタイトル、**ターゲット文字セットの種類**特定の文字セットのマッピングの設定が含まれています。 この列の値は次のとおりです。  
  
        -   CHAR と VARCHAR  
  
        -   NCHAR と NVARCHAR  
  
    > [!IMPORTANT]  
    > 特定の文字セットの既定値では、CHAR/VARCHAR、NCHAR/NVARCHAR、または後に、プレフィックス (既定) があります。  
  
    MySQL データベースとメタデータのルート ノード レベルでターゲット データベース間で文字セットのマッピングは次のとおりです。  
  
    ||||  
    |-|-|-|  
    |**文字セットの名前**|**文字セットの説明**|**ターゲット文字セットの種類 (既定値)**|  
    |big5|Big5 繁体字中国語|NCHAR と NVARCHAR (既定値)|  
    |dec8|DEC 西ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |cp850|DOS 西ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |hp8|HP 西ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |koi8r|KOI8 R Relcom ロシア語|CHAR と VARCHAR (既定値)|  
    |ラテン 1|cp1252 西ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |latin2|ISO 8859-2 中央ヨーロッパ言語|CHAR と VARCHAR (既定値)|  
    |swe7|7 ビット スウェーデン語|CHAR と VARCHAR (既定値)|  
    |Ascii|US-ASCII|CHAR と VARCHAR (既定値)|  
    |ujis|EUC-JP 日本語|NCHAR と NVARCHAR (既定値)|  
    |sjis|Shift JIS の日本語|NCHAR と NVARCHAR (既定値)|  
    |ヘブライ語|ISO 8859-8 ヘブライ語|CHAR と VARCHAR (既定値)|  
    |tis620|TIS620 タイ語|CHAR と VARCHAR (既定値)|  
    |euckr|EUC-KR 韓国語|NCHAR と NVARCHAR (既定値)|  
    |koi8u|KOI8-u ウクライナ語|CHAR と VARCHAR (既定値)|  
    |gb2312|GB2312 簡体字中国語|NCHAR と NVARCHAR (既定値)|  
    |ギリシャ語|ISO 8859-7 ギリシャ語|CHAR と VARCHAR (既定値)|  
    |cp 1250|中央ヨーロッパ言語の Windows|CHAR と VARCHAR (既定値)|  
    |gbk|GBK 簡体字中国語|NCHAR と NVARCHAR (既定値)|  
    |ラテン 5|ISO 8859-3 トルコ語|CHAR と VARCHAR (既定値)|  
    |armscii8|ARMSCII 8 アルメニア語|CHAR と VARCHAR (既定値)|  
    |utf8|Utf-8 の Unicode|NCHAR と NVARCHAR (既定値)|  
    |ucs2|Unicode の ucs-2|NCHAR と NVARCHAR (既定値)|  
    |cp866|DOS のロシア語|CHAR と VARCHAR (既定値)|  
    |keybcs2|DOS Kamenicky チェコ語、スロバキア語|CHAR と VARCHAR (既定値)|  
    |macce|Mac の中央ヨーロッパ言語|CHAR と VARCHAR (既定値)|  
    |macroman|Mac 西ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |cp852|DOS 中央ヨーロッパ|CHAR と VARCHAR (既定値)|  
    |latin7|ISO 8859-13 バルト言語|CHAR と VARCHAR (既定値)|  
    |cp 1251|Windows キリル語|CHAR と VARCHAR (既定値)|  
    |cp 1256|Windows のアラビア語|CHAR と VARCHAR (既定値)|  
    |cp 1257|Windows バルト言語|CHAR と VARCHAR (既定値)|  
    |バイナリ|バイナリの疑似文字セット|CHAR と VARCHAR (既定値)|  
    |geostd8|GEOSTD8 グルジア語|CHAR と VARCHAR (既定値)|  
    |cp932|Windows 日本語 SJIS|NCHAR と NVARCHAR (既定値)|  
    |eucjpms|Windows 日本語 UJIS|NCHAR と NVARCHAR (既定値)|  
  
2.  **データベース、カテゴリまたはノード レベルのオブジェクト。** データベース、カテゴリ、またはオブジェクト ノード レベルでは、マッピング グリッド charset には行が含まれて、同じルート メタデータ ノード レベルで 1 つとして可視。  
  
    1.  タイトル、グリッドの最初の列**文字セット名**文字セットの名前が含まれています。  
  
    2.  2 番目の列のタイトル、**文字セットの説明**文字セットの説明が含まれています。  
  
    3.  唯一の違いは、グリッドの 3 番目の列の値です。 3 番目の列のタイトル、**対象のデータ型**特定の文字セットのマッピングの設定が含まれています。 列の値は次のとおりです。  
  
        -   継承 (CHAR と VARCHAR または NCHAR または NVARCHAR)  
  
        -   CHAR と VARCHAR  
  
        -   NCHAR と NVARCHAR  
  
> [!IMPORTANT]  
> -   MySQL データベースとデータベース、カテゴリ、およびオブジェクト ノード レベルでターゲット データベース間で文字セットのマッピングでは、既定の値列のルート以外の各レベルで特定の文字セットの**対象のデータ型**する必要があります '継承された '。  
> -   グリッドの値で**継承された**いずれかのサフィックスが '(CHAR/VARCHAR)' または '(NCHAR/NVARCHAR)' によって値がこの特定の文字セットによって親から継承されました。  
  
