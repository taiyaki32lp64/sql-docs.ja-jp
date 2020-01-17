---
title: bcp を使用したフィールド長の指定 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- native data format [SQL Server]
- default field lengths
- field length [SQL Server]
- data formats [SQL Server], field length
- bcp utility [SQL Server], field length
ms.assetid: 240f33ca-ef4a-413a-a4de-831885cb505b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: abb451611f7e102e9167561ef2c3a4b64e00fb12
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66011838"
---
# <a name="specify-field-length-by-using-bcp-sql-server"></a>bcp を使用したフィールド長の指定 (SQL Server)
  フィールド長は、文字形式でデータを表現するために必要な文字の最大数を示します。 データがネイティブ形式で格納されている場合、フィールド長は既にわかっています。たとえば、`int` データ型では 4 バイトになります。 プレフィックス長に 0 を指定した場合、 **bcp**コマンドによってフィールド長、既定のフィールド長、および含んでいるデータ ファイル内のデータ ストレージに対するフィールド長の影響のプロンプトが`char`データ。  
  
## <a name="the-bcp-prompt-for-field-length"></a>フィールド長を要求する bcp プロンプト  
 対話型の **bcp** コマンドで、フォーマット ファイル スイッチ ( **-f**) またはデータ形式スイッチ ( **-n**、 **-c**、 **-w** または **-N**) のどちらも付けずに **in** または **out** オプションを指定すると、次のように各データ フィールドの長さを要求するプロンプトが表示されます。  
  
 `Enter length of field <field_name> [<default>]:`  
  
 コンテキスト内でこのプロンプトが表示される例については、「[bcp を使用した互換性のためのデータ形式の指定 &#40;SQL Server&#41;](specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)」を参照してください。  
  
> [!NOTE]  
>  **bcp** コマンドですべてのフィールドを対話形式で指定すると、各フィールドへの応答を XML 形式以外のファイルに保存するように要求するプロンプトが表示されます。 XML 以外のフォーマット ファイルの詳細については、「[XML 以外のフォーマット ファイル &#40;SQL Server&#41;](xml-format-files-sql-server.md)」を参照してください。  
  
 **bcp** コマンドでフィールド長を要求するプロンプトが表示されるかどうかは、次のさまざまな要素によって決まります。  
  
-   固定長でないデータ型のコピー時にプレフィックス長を 0 に指定した場合、 **bcp** によってフィールド長を要求するプロンプトが表示されます。  
  
-   非文字データを文字データに変換するとき、 **bcp** によってデータの保存に十分な長さの既定フィールド長が提示されます。  
  
-   ファイル保存形式が非文字である場合、 **bcp** コマンドによってフィールド長を要求するプロンプトは表示されません。 データは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のネイティブ データ表現 (ネイティブ形式) で保存されます。  
  
## <a name="using-default-field-lengths"></a>既定のフィールド長の使用  
 通常、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] では、 **bcp**によって提示された既定値をフィールド長に使用することをお勧めします。 キャラクター モードのデータ ファイルが作成された場合、既定のフィールド長を使用することによって、データの切り捨てや数値オーバーフロー エラーの発生を防止できます。  
  
 不適切なフィールド長を指定すると、問題が発生する場合があります。 たとえば、数値データをコピーするときに、そのデータに対して短すぎるフィールド長を指定すると、 **bcp** ユーティリティによってオーバーフロー エラー メッセージが出力され、データはコピーされません。 また、エクスポートする場合は`datetime`データの文字列に対して 26 バイトよりも短いフィールド長を指定し、 **bcp**ユーティリティには、エラー メッセージなしでデータが切り捨てられます。  
  
> [!IMPORTANT]  
>  既定のサイズ オプションを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は文字列全体を読み取ります。 場合によっては、既定のフィールド長を使用すると、"予期しないファイルの終了" エラーが発生することもあります。 通常は、このエラーが発生します、`money`と`datetime`データ型は、データ ファイルで、予期されるフィールドの一部だけが発生したときなど、`datetime`の値*mm*/*dd* / *yy* 、時刻部分なしで指定され、は、そのための予期される 24 文字の長さより短い、`datetime`値`char`形式。 この種類のエラーを防止するには、フィールド ターミネータまたは固定長データ フィールドを使用するか、既定のフィールド長を別の値に変更します。  
  
### <a name="default-field-lengths-for-character-file-storage"></a>文字ファイル保存の既定のフィールド長  
 次の表は、文字ファイル保存形式として保存されるデータの既定のフィールド長を示しています。 NULL 値を使用できるデータの長さは、NULL 値を使用できないデータの長さと同じです。  
  
|データ型|既定の長さ (文字数)|  
|---------------|-----------------------------------|  
|`char`|列に対して定義された長さ|  
|`varchar`|列に対して定義された長さ|  
|`nchar`|列に対して定義された長さの 2 倍|  
|`nvarchar`|列に対して定義された長さの 2 倍|  
|`Text`|0|  
|`ntext`|0|  
|`bit`|1|  
|`binary`|列に対して定義された長さの 2 倍 + 1|  
|`varbinary`|列に対して定義された長さの 2 倍 + 1|  
|`image`|0|  
|`datetime`|24|  
|`smalldatetime`|24|  
|`float`|30|  
|`real`|30|  
|`int`|12|  
|`bigint`|19|  
|`smallint`|7|  
|`tinyint`|5|  
|`money`|30|  
|`smallmoney`|30|  
|`decimal`|41*|  
|`numeric`|41*|  
|`uniqueidentifier`|37|  
|`timestamp`|17|  
|`varchar(max)`|0|  
|`varbinary(max)`|0|  
|`nvarchar(max)`|0|  
|UDT (UDT)|ユーザー定義型 (UDT) 列の長さ|  
|XML|0|  
  
 \*詳細については、`decimal`と`numeric`、データ型を参照してください[decimal および numeric &#40;TRANSACT-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)します。  
  
> [!NOTE]  
>  `tinyint` 型の列には、0 ～ 255 の値を入力できます。この範囲の任意の数を表現するために必要な最大文字数は 3 です。これは、100 ～ 255 に相当します。  
  
### <a name="default-field-lengths-for-native-file-storage"></a>ネイティブ ファイル保存の既定のフィールド長  
 次の表は、ネイティブ ファイル保存形式として保存されるデータの既定のフィールド長を示しています。 NULL 値を使用できるデータの長さは、NULL 値を使用できないデータの長さと同じです。また、文字データは常に文字形式で保存されます。  
  
|データ型|既定の長さ (文字数)|  
|---------------|-----------------------------------|  
|`bit`|1|  
|`binary`|列に対して定義された長さ|  
|`varbinary`|列に対して定義された長さ|  
|`image`|0|  
|`datetime`|8|  
|`smalldatetime`|4|  
|`float`|8|  
|`real`|4|  
|`int`|4|  
|`bigint`|8|  
|`smallint`|2|  
|`tinyint`|1|  
|`money`|8|  
|`smallmoney`|4|  
|`decimal` <sup>1</sup>|<sup>*</sup>|  
|`numeric` <sup>1</sup>|<sup>*</sup>|  
|`uniqueidentifier`|16|  
|`timestamp`|8|  
  
 <sup>1</sup>の詳細については、`decimal`と`numeric`、データ型を参照してください[decimal および numeric &#40;TRANSACT-SQL&#41;](/sql/t-sql/data-types/decimal-and-numeric-transact-sql)します。  
  
 前述のすべての場合に、後で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に再読み込みするためにデータ ファイルを作成して、保存領域を最小限に抑えるには、既定のファイル保存形式と既定のフィールド長と共に、フィールド長プレフィックスを使用します。  
  
## <a name="see-also"></a>関連項目  
 [bcp ユーティリティ](../../tools/bcp-utility.md)   
 [データ型 &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql)   
 [フィールド ターミネータと行ターミネータの指定 &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)   
 [bcp を使用したデータ ファイルのプレフィックス長の指定 &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)   
 [bcp を使用したファイル ストレージ型の指定 &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)   
 [一括インポート中の NULL の保持または既定値の使用 &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
  
