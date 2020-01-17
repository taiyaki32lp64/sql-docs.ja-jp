---
title: ルール、トリガー、既定値、およびストアド プロシージャのサポート |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 90a39ad540f3320ed78e981030679b59d911eeef
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080774"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>ルール、トリガー、既定値、およびストアド プロシージャのサポート (Visual FoxPro ODBC ドライバー)
Visual FoxPro ルール、トリガー、既定値、または、Visual FoxPro ODBC ドライバーを使用してストアド プロシージャを作成することはできません。 ただし、挿入、更新、またはデータベースに格納されている Visual FoxPro データを削除すると、アプリケーションは既存のルール、トリガー、既定値、またはストアド プロシージャとやり取りします。  
  
 次の表には、Visual FoxPro コマンドとコマンドまたは関数は、ルール、トリガー、既定値、またはストアド プロシージャが存在する場合は、Visual FoxPro ODBC ドライバーでサポートされている関数が一覧表示します。  
  
 ルール、トリガー、既定値にデータをやり取りするアプリケーションまたはストアド プロシージャを呼び出す他の Visual FoxPro コマンドまたは関数は、ドライバーはエラーを生成します。 参照してください[サポートされていない Visual FoxPro コマンドと関数](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md)コマンドと、ドライバーによってサポートされていない関数の一覧についてはします。  
  
> [!TIP]  
>  使用することができます、ルール、トリガー、または、ドライバーによって呼び出されたときに実行するコマンドを決定するストアド プロシージャに条件付きのコードを挿入する場合、**バージョン ()** 関数。 **バージョン ()** 関数が返される"Visual FoxPro ODBC ドライバー *\<バージョン >* "ドライバーによって呼び出されるとします。  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Visual FoxPro コマンドと規則、トリガー、既定値、およびストアド プロシージャでサポートされる関数  
  
||||  
|-|-|-|  
|$ 演算子|% 演算子|(& A) コマンド|  
|& & コマンド|* コマンド|= コマンド|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS () 関数|ACOPY () 関数|TABLE コマンドを追加します。|  
|ADATABASES () 関数|ADBOBJECTS () 関数|待ち () 関数|  
|ADEL () 関数|AELEMENT () 関数|ALEN () 関数|  
|AFIELDS () 関数|AINS () 関数|ALTER TABLE - SQL コマンド|  
|エイリアス () 関数|ALLTRIM () 関数|配列のコマンドを追加します。|  
|AND 演算子|コマンドを追加します。|メモのコマンドを追加します。|  
|コマンドを追加します。|[全般] のコマンドを追加します。|ASCAN () 関数|  
|プロシージャのコマンドを追加します。|ASC () 関数|ASUBSCRIPT () 関数|  
|ASIN () 関数|ASORT () 関数|ATAN () 関数|  
|() 関数|AT_C () 関数|ATCLINE () 関数|  
|ATC () 関数|ATCC () 関数|AUSED () 関数|  
|ATLINE () 関数|ATN2 () 関数||  
|平均コマンド|ACOS () 関数||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|トランザクション コマンドを開始します。|() 関数の間|BITNOT () 関数|  
|BITCLEAR () 関数|BITLSHIFT () 関数|ビットセット () 関数|  
|BITOR () 関数|BITRSHIFT () 関数|空のコマンド|  
|BITTEST () 関数|BITXOR () 関数||  
|BOF () 関数|BITAND () 関数||  
  
## <a name="c"></a>c  
  
||||  
|-|-|-|  
|コマンドを計算します。|候補者 () 関数|CHR () 関数|  
|CDX () 関数|CEILING () 関数|閉じるコマンド|  
|CHRTRAN () 関数|CHRTRANC () 関数|インデックスのコピー コマンド|  
|CMONTH () 関数|コマンドを続行します。|コピー構造拡張コマンド|  
|プロシージャのコマンドをコピーします。|構造体のコマンドをコピーします。|コマンドにコピーします。|  
|タグ コマンドをコピーします。|コマンドの配列にコピーします。|CPCONVERT () 関数|  
|COS () 関数|カウント コマンド|CTOD () 関数|  
|CPCURRENT () 関数|CPDBF () 関数|CURSORSETPROP () 関数|  
|CTOT () 関数|CURSORGETPROP () 関数||  
|CURVAL () 関数|CDOW () 関数||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|日付 () 関数|DATETIME () 関数|DAY () 関数|  
|DBC () 関数|DBF () 関数|DBGETPROP () 関数|  
|DBUSED () 関数|DELETE - SQL コマンド|コマンドを削除します。|  
|DELETE TAG コマンド|削除された () 関数|降順 () 関数|  
|相違点 () 関数|ディメンション コマンド|ディスク容量 () 関数|  
|DMY () 関数|ケースを実行してください...ENDCASE コマンド|コマンドの操作を行います|  
|実行中にしてください...ENDDO コマンド|DOW () 関数|DTOC () 関数|  
|DTOR () 関数|DTO () 関数|DTOT () 関数|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|空の () 関数|() 関数を評価します。|EXIT コマンド|  
|エラー () 関数|EXP () 関数||  
|トランザクションのコマンドの終了|EOF () 関数||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT () 関数|FDATE () 関数|フィールド () 関数|  
|ファイル () 関数|フィルター () 関数|FLDLIST () 関数|  
|群れ () 関数|FLOOR () 関数|フラッシュ コマンド|  
|FOR...ENDFOR コマンド|() 関数|() 関数が見つかりました|  
|無料の TABLE コマンド|FSIZE () 関数|FTIME () 関数|  
|FULLPATH () 関数|関数のコマンド|() 関数|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|コマンドを収集します。|GETNEXTMODIFIED () 関数|移動/[ジャンプ] コマンド|  
|GETFLDSTATE () 関数|GOMONTH () 関数||  
|GETCP () 関数|GETENV () 関数||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|ヘッダー () 関数|HOUR () 関数|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE () 関数|もし...ENDIF コマンド|IIF () 関数|  
|INDBC () 関数|INDEX コマンド|引数が極端に () 関数|  
|INSERT SQL コマンド|INT () 関数|ISALPHA () 関数|  
|ISBLANK () 関数|ISDIGIT () 関数|ISEXCLUSIVE () 関数|  
|ISLEADBYTE () 関数|ISLOWER () 関数|ISNULL () 関数|  
|ISREADONLY () 関数|ISUPPER () 関数||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|キー () 関数|KEYMATCH () 関数||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|左 () 関数|LEFTC () 関数|LIKEC () 関数|  
|LENC () 関数|() 関数のように|ロック () 関数|  
|ローカル コマンド|コマンドを見つける|参照 () 関数|  
|ログ () 関数|LOG10 () 関数|LTRIM () 関数|  
|LOWER () 関数|LPARAMETERS コマンド||  
|LUPDATE () 関数|LEN () 関数||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE システム メモリ変数|MAX () 関数|MDX () 関数|  
|年 (mdy) に関するページ () 関数|MEMLINES () 関数|メッセージ () 関数|  
|MIN () 関数|分 () 関数|MLINE () 関数|  
|MOD () 関数|月 () 関数|MTON () 関数|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX () 関数|() 関数を正規化します。|NOT 演算子|  
|注コマンド|NTOM () 関数|NVL () 関数|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|() 関数に発生します|ない () 関数|エラー コマンド|  
|キー コマンド|() 関数|データベースを開くコマンド|  
|OR 演算子|順序 () 関数|OS () 関数|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK コマンド|パラメーター () 関数|支払いに関するページ () 関数|  
|コマンドのパラメーター|プライマリ () 関数|プライベート コマンド|  
|PI () 関数|プログラム () 関数|適切な () 関数|  
|PROCEDURE コマンド|PV () 関数||  
|パブリック コマンド|PADL ()&#124;して、PADR () &#124; PADC () 関数||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND () 関数|RAT () 関数|RATC () 関数|  
|RATLINE () 関数|コマンドを取り消し|RECCOUNT () 関数|  
|RECNO () 関数|RECSIZE () 関数|地域コマンド|  
|リレーションシップ () 関数|テーブル コマンドを削除します。|REPLACE コマンド|  
|配列のコマンドからの置換します。|REPLICATE () 関数|コマンドを再試行してください。|  
|コマンドを返す|右 () 関数|RIGHTC () 関数|  
|リソース ロック () 関数|ROLLBACK コマンド|ROUND () 関数|  
|RTOD () 関数|RTRIM () 関数||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|スキャンしています...ENDSCAN コマンド|コマンドを散布図します。|秒 () 関数|  
|秒 () 関数|コマンドにシークします。|シーク () 関数|  
|コマンドを選択します。|選択 () 関数|SQL コマンド|  
|SET BLOCKSIZE コマンド|SET キャリー コマンド|SET 世紀コマンド|  
|SET COLLATE コマンド|データベース コマンドのセット|DATE コマンドのセット|  
|セットの既定のコマンド|SET DELETED コマンド|SET EXACT コマンド|  
|SET EXCLUSIVE コマンド|SET FDOW コマンド|フィールドの SET コマンド|  
|フィルターの SET コマンド|固定の SET コマンド|SET FULLPATH コマンド|  
|SET FWEEK コマンド|時間の設定コマンド|インデックスの SET コマンド|  
|SET LOCK コマンド|SET MULTILOCKS コマンド|コマンドの近くに設定します|  
|SET NOCPTRANS コマンド|通知コマンドのセット|SET NULL コマンド|  
|SET の最適化のコマンド|セットの順序コマンド|SET PATH コマンド|  
|SET プロシージャ コマンド|SET 関係コマンド|関係の設定 コマンドをオフ|  
|SET REPROCESS コマンド|[スキップ] コマンドを設定します。|SET UDFPARMS コマンド|  
|SET UNIQUE コマンド|SET ボリューム コマンド|設定 () 関数|  
|SETFLDSTATE () 関数|SIGN () 関数|SIN () 関数|  
|[スキップ] コマンド|SORT コマンド|スペース () 関数|  
|SQRT () 関数|ストア コマンド|STR () 関数|  
|STRCONV () 関数|STRTRAN () 関数|STUFF () 関数|  
|STUFFC () 関数|SUBSTR () 関数|SUBSTRC () 関数|  
|合計コマンド|SYS(2011) 関数||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY システム メモリ変数|_TRIGGERLEVEL システム メモリ変数|TAGCOUNT () 関数|  
|TABLEUPDATE () 関数|タグ () 関数|対象の () 関数|  
|TAGNO () 関数|TAN () 関数|TRIM () 関数|  
|時間 () 関数|合計コマンド|TXNLEVEL () 関数|  
|TTOC () 関数|TTOD () 関数||  
|型 () 関数|TABLEREVERT () 関数||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|一意の () 関数|コマンドのロックを解除します。|コマンドを使用します。|  
|UPDATE コマンド|上部 () 関数||  
|() 関数の使用|UPDATE - SQL コマンド||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL () 関数|バージョン () 関数||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|週 () 関数|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR () 関数|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP コマンド|||
