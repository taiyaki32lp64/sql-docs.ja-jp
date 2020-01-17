---
title: Schema.ini ファイル (テキスト ファイル ドライバー) |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema.ini file [ODBC]
- text file driver [ODBC], schema.ini file
ms.assetid: 0c4625c4-c730-4984-b430-9051b7bc0451
author: MightyPen
ms.author: genemi
ms.openlocfilehash: dd95329c91c69af38b1ffc7951191498fcc40479
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67987947"
---
# <a name="schemaini-file-text-file-driver"></a>Schema.ini ファイル (テキスト ファイル ドライバー)
テキストのドライバーを使用する場合、スキーマ情報ファイルを使用してテキスト ファイルの形式が決まります。 スキーマの情報ファイルは常に Schema.ini という名前し、常にテキスト データ ソースと同じディレクトリに保持されます。 スキーマの情報ファイルは、ファイル、列名とデータ型情報、およびその他のいくつかのデータの特性の一般的な形式に関する情報を IISAM を提供します。 Schema.ini ファイルは、固定長データにアクセスするために必要では常にします。 テキスト、テーブルには、DateTime、通貨、または 10 進数データ、またはいつでも、テーブル内のデータの処理を制御することが含まれている場合、Schema.ini ファイルを使用する必要があります。  
  
> [!NOTE]  
>  レジストリから、Schema.ini からではなく、テキスト ISAM は初期値を取得します。 同じ既定のファイル形式は、すべての新しいテキスト データ テーブルに適用されます。 CREATE TABLE ステートメントによって作成されたすべてのファイルは継承これら同じ既定の形式の値でのファイル形式の値を選択して設定される、**テキスト形式の定義** ダイアログ ボックスで\<既定 >、でを選択して**テーブル**一覧。 レジストリの値は、Schema.ini の値と異なる場合、Schema.ini の値によって、レジストリの値が上書きされます。  
  
## <a name="understanding-schemaini-files"></a>Schema.ini ファイルをについてください。  
 Schema.ini ファイルでは、テキスト ファイル内のレコードに関するスキーマ情報を提供します。 Schema.ini の各エントリでは、テーブルの 5 つの特性の 1 つを指定します。  
  
-   テキスト ファイルの名前  
  
-   ファイルの形式  
  
-   フィールド名、幅、および種類  
  
-   文字セット  
  
-   特別なデータ型の変換  
  
 次のセクションでは、これらの特性について説明します。  
  
## <a name="specifying-the-file-name"></a>ファイル名を指定します。  
 Schema.ini の最初のエントリは、常に角かっこで囲まれたテキストのソース ファイルの名前です。 次の例は、Sample.txt ファイルのエントリを示しています。  
  
```  
[Sample.txt]  
```  
  
## <a name="specifying-the-file-format"></a>ファイル形式を指定します。  
 **形式**Schema.ini でオプションをテキスト ファイルの形式を指定します。 Text IISAM は文字で区切られたファイルから自動的に書式を読み取ることができます。 任意の 1 文字は、二重引用符 (") を除く、ファイル内の区切り記号として使用できます。 **形式**Schema.ini の設定は、Windows レジストリ、ファイルごとの設定をオーバーライドします。 次の表に、有効な値、**形式**オプション。  
  
|書式指定子|テーブルの形式|Schema.ini Format ステートメント|  
|----------------------|------------------|---------------------------------|  
|**タブ区切り**|ファイル内のフィールドはタブで区切られます。|形式 TabDelimited を =|  
|**CSV の区切り**|ファイル内のフィールドはコンマ (コンマ区切り値) で区切られます。|形式 = CSVDelimited|  
|**区切り文字**|ファイル内のフィールドは、ダイアログ ボックスへの入力に選択した任意の文字で区切られます。 二重引用符 (") 以外のすべてが許可されている、空白を含むです。|形式 = 区切り記号 (*カスタム文字*)<br /><br /> \- または -<br /><br /> 区切り記号なしで次のように指定します。<br /><br /> Format=Delimited( )|  
|**固定長**|ファイル内のフィールドでは、固定長です。|形式 FixedLength を =|  
  
## <a name="specifying-the-fields"></a>フィールドの指定  
 2 つの方法でテキストの文字で区切られたファイルでは、フィールド名を指定できます。  
  
-   テーブルの最初の行にフィールド名を含めるし、設定**ColNameHeader**に**True です。**  
  
-   各列番号を指定し、列名とデータ型を指定します。  
  
 番号では、各列を指定し、列名、データ型、および固定長ファイルの幅を指定する必要があります。  
  
> [!NOTE]  
>  **ColNameHeader** Schema.ini 上書きの設定、**消えて**Windows レジストリ、ファイルごとに設定します。  
  
 フィールドのデータ型も確認できます。 使用して、 **MaxScanRows**オプションを示す列の型を決定するときに、行の数をスキャンする必要があります。 設定した場合**MaxScanRows**ファイル全体をスキャンする 0 にします。 **MaxScanRows** Schema.ini の設定は、Windows レジストリ、ファイルごとの設定をオーバーライドします。  
  
 次のエントリは、Microsoft Jet は、テーブルの最初の行でデータを使用して、フィールド名を決定する必要があり、データを決定ファイル全体を調べる必要があることを示します。 使用される型。  
  
```  
ColNameHeader=True  
MaxScanRows=0  
```  
  
 次のエントリは、列番号を使用してテーブル内のフィールドを指定 (**Col**_n_) 文字で区切られたファイルの省略可能で、固定長ファイルに必要なのオプションです。 例では、2 つのフィールド、10 文字の列名を CustomerNumber テキスト フィールドおよび 30 文字 CustomerName テキスト フィールド、Schema.ini のエントリを示します。  
  
```  
Col1=CustomerNumber Text Width 10  
Col2=CustomerName Text Width 30  
```  
  
 構文**Col**_n_は。  
  
```  
  
n=ColumnNametype [#]  
```  
  
## <a name="remarks"></a>コメント  
 次の表の各部分の説明、 **Col**_n_エントリ。  
  
|パラメーター|説明|  
|---------------|-----------------|  
|*[ColumnName]*|列のテキストの名前。 列名にスペースが含まれている場合は、二重引用符で囲む必要があります。|  
|*type*|データ型は次のとおりです。<br /><br /> **Microsoft Jet データ型**<br /><br /> ビット<br /><br /> バイト<br /><br /> Short<br /><br /> Long<br /><br /> 通貨<br /><br /> 単一<br /><br /> Double<br /><br /> DateTime<br /><br /> テキスト<br /><br /> メモ<br /><br /> **ODBC データ型**Char (テキストと同じ)<br /><br /> Float (Double と同じ)<br /><br /> 整数 (短い形式と同じ)<br /><br /> LongChar (メモ型と同じ)<br /><br /> 日付*日付形式*|  
|**Width**|リテラル文字列値`Width`します。 次の数が列の幅を指定することを示します (ファイルの文字で区切られた省略可能です。 固定長ファイルに必要)。|  
|*#*|列の幅を指定する整数値 (必要な場合**幅**を指定)。|  
  
## <a name="selecting-a-character-set"></a>文字セットの選択  
 2 つの文字セットから選択できます。ANSI、OEM です。 **CharacterSet** Schema.ini の設定は、Windows レジストリ、ファイルごとの設定をオーバーライドします。 次の例では、ANSI に設定する文字を設定する Schema.ini エントリを示します。  
  
```  
CharacterSet=ANSI  
```  
  
## <a name="specifying-data-type-formats-and-conversions"></a>データ型の形式と変換を指定します。  
 Schema.ini ファイルには、データを変換または表示する方法を指定するのに使用できるいくつかのオプションが含まれています。 次の表には、これらの各オプションが一覧表示します。  
  
|OPTION|説明|  
|------------|-----------------|  
|**DateTimeFormat**|日付と時刻を示す書式指定文字列に設定できます。 インポート/エクスポート内のすべての日付/時刻フィールドが同じ形式で処理される場合は、このエントリを指定する必要があります。 午前を除くすべての Microsoft Jet 形式 および p. m. サポートされます。 書式指定文字列がない場合は、Windows コントロール パネルの短い日付画像と時間のオプションが使用されます。|  
|**DecimalSymbol**|数値の小数部からの整数を分離するために使用する任意の 1 文字に設定できます。|  
|**NumberDigits**|数値の小数部分の 10 進数字の数を示します。|  
|**NumberLeadingZeros**|1 より小さい、-1 以上の 10 進数の値が先頭に 0 を含めるかどうかを指定します。この値は False (先行ゼロを付けない)、または True です。|  
|**CurrencySymbol**|通貨値のテキスト ファイルで使用できる通貨記号を示します。 例には、Dm、ドル記号 ($) が含まれます。|  
|**CurrencyPosFormat**|次の値のいずれかに設定できます。<br /><br /> 、($1) を分離せずに通貨記号のプレフィックス<br />、分離せずに通貨記号のサフィックス (1$)<br />の 1 文字分 ($ 1) 通貨記号のプレフィックス<br />通貨記号のサフィックスが 1 文字分 (1 $)|  
|**CurrencyDigits**|通貨値の小数部分を使用する桁数を指定します。|  
|**CurrencyNegFormat**|次の値のいずれかです。<br /><br /> -   ($1)<br />--$1<br />-$1<br />-1-<br />-   (1$)<br />--1$<br />-1$<br />-$ 1-<br />--1 $<br />--$ 1<br />-$ 1-<br />-1-<br />-$-1<br />-1 $<br />-   ($ 1)<br />-   (1 $)<br /><br /> この例には、ドル記号が表示されますが、適切な置換する必要があります**CurrencySymbol**実際のプログラム内の値。|  
|**CurrencyThousandSymbol**|数千ものが、テキスト ファイル内の通貨値を区切るために使用できる 1 文字の記号を示します。|  
|**CurrencyDecimalSymbol**|通貨値の小数部から全体を分離するために使用する任意の 1 文字に設定できます。|  
  
> [!NOTE]  
>  エントリを省略した場合は、Windows コントロール パネルの 既定値が使用されます。
