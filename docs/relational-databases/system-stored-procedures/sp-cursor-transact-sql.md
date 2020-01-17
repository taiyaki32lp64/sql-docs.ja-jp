---
title: sp_cursor (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursor_TSQL
- sp_cursor
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursor
ms.assetid: 41ade0ca-5f11-469d-bd4d-c8302ccd93b3
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd5cae24b30840ea08ec2ae025b021fcf70f2dc6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108574"
---
# <a name="spcursor-transact-sql"></a>sp_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  位置指定更新を要求します。 このプロシージャは、カーソルのフェッチ バッファー内にある 1 つ以上の行に対して操作を実行します。 sp_cursor は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットでは 1 を = です。  
  
||  
|-|  
|**適用対象**:SQL Server ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]を通じて[現在のバージョン](https://go.microsoft.com/fwlink/p/?LinkId=299658))。|  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursor  cursor, optype, rownum, table  
    [ , value[...n]]]  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 カーソル ハンドルです。 *カーソル*が必要なパラメーターです、 **int**値を入力します。 *カーソル*は、*処理*値は SQL Server によって生成され、sp_cursoropen プロシージャから返されます。  
  
 *optype*  
 実行は、カーソル操作を指定する必須パラメーターです。 *optype* 、次のいずれかが必要です**int**値を入力します。  
  
|値|名前|説明|  
|-----------|----------|-----------------|  
|0X0001|UPDATE|フェッチ バッファー内の 1 つまたは複数の行を更新するには、使用されます。  指定されている行*rownum*は、再アクセス、更新します。|  
|0x0002|Del|フェッチ バッファー内の 1 つまたは複数の行を削除に使用されます。 指定されている行*rownum*再アクセス、削除されます。|  
|0X0004|INSERT|SQL をビルドせずにデータを挿入**挿入**ステートメント。|  
|0X0008|更新|基になるテーブルのバッファーを補充するために使用して、更新プログラムの場合、行を更新または削除できないオプティミスティック同時実行制御、または更新後に使用できます。|  
|0X10|ロック|SQL Server U ロックを指定された行が含まれるページに獲得されるが発生します。 このロックは互換性のある、X ロックやその他の U ロックと S ロックします。 短期間のロックを実装する場合に使用できます。|  
|0X20|SETPOSITION|DELETE または UPDATE ステートメントを配置してプログラムを後続の SQL server を実行するときにのみ使用されます。|  
|0X40|ABSOLUTE|UPDATE または DELETE との組み合わせでのみ使用できます。  ABSOLUTE は KEYSET カーソルでのみ使用されます (DYNAMIC カーソルでは無視されます。STATIC カーソルは更新できません)。<br /><br /> 注:絶対フェッチされていないキーセット内の行を指定すると、操作の同時実行制御チェックが失敗し、返される結果は保証できません。|  
  
 *rownum*  
 これはフェッチ バッファー内の行の操作、更新、または削除は、カーソルを指定します。  
  
> [!NOTE]  
>  これは、RELATIVE、NEXT、または PREVIOUS のフェッチ操作、更新や sp_cursor を使用して実行された削除の開始点には影響しません。  
  
 *rownum*が必要なパラメーターです、 **int**値を入力します。  
  
 1  
 フェッチ バッファー内の最初の行を示します。  
  
 2  
 フェッチ バッファー内の 2 つ目の行を示します。  
  
 3、4、5  
 3 番目、4 番目、5 番目の行を示します。  
  
 n  
 フェッチ バッファー内の n 番目の行を示します。  
  
 0  
 フェッチ バッファー内のすべての行を示します。  
  
> [!NOTE]  
>  更新、削除、更新、またはロックで使用するために有効なのみ*optype*値。  
  
 *テーブル*  
 テーブルを識別するテーブル名を*optype*カーソル定義は、結合を含むまたはあいまいな列名がによって返されるときに適用される、*値*パラメーター。 特定のテーブルを指定しない場合、既定値は FROM 句の最初のテーブルになります。 *テーブル*文字列入力値を必要とする省略可能なパラメーターです。 文字列は、任意の文字または UNICODE データ型として指定できます。 *テーブル*マルチパートのテーブル名を指定できます。  
  
 *value*  
 値を挿入または更新する場合に使用します。 *値*文字列パラメーターは、UPDATE および INSERT でのみ使用*optype*値。 文字列は、任意の文字または UNICODE データ型として指定できます。  
  
> [!NOTE]  
>  パラメーター名*値*ユーザーが割り当てることができます。  
  
## <a name="return-code-values"></a>リターン コードの値  
 バッファー番号 0 の位置指定の DELETE または UPDATE 操作が含む DONE メッセージを返す、RPC を使用する場合、 *rowcount* 0 (失敗) またはフェッチ バッファー内の行ごとに 1 (成功)。  
  
## <a name="remarks"></a>コメント  
  
## <a name="optype-parameter"></a>optype パラメーター  
 SETPOSITION と更新、削除、更新、またはロックの組み合わせを除く絶対と UPDATE または DELETE、または、 *optype*値は相互に排他的です。  
  
 更新の値の SET 句がから構築された、*値*パラメーター。  
  
 INSERT を使用する利点の 1 つ*optype*値が非文字データ挿入のための文字形式に変換するを回避することができます。 値は、更新プログラムと同じ方法で指定されます。 必須の列が含まれていない場合、INSERT は失敗します。  
  
-   SETPOSITION の値は、RELATIVE、NEXT、または PREVIOUS のフェッチ操作の開始位置や、sp_cursor インターフェイスを使用して実行される更新や削除には影響しません。 フェッチ バッファー内の行を指定していない任意の数は、エラーは返されません 1 に設定されている位置になります。 SETPOSITION を実行すると、位置を次の sp_cursorfetch 操作、T-SQL まで有効になります**フェッチ**操作、または sp_cursor SETPOSITION の操作、同じカーソルを使用します。 Sp_cursorfetch 操作が他のカーソル呼び出しは位置の値に影響しませんは、新しいフェッチ バッファー内の最初の行にカーソルの位置を設定します。 最後に変更された行の位置の値を設定するには、更新、UPDATE、DELETE、または LOCK を OR 句で SETPOSITION をリンクできます。  
  
 を介してフェッチ バッファー内の行が指定されていない場合、 *rownum*パラメーター位置は、返されるエラーの 1 に設定されます。 設定された位置は、同じカーソルを使用して次の sp_cursorfetch 操作、T-SQL FETCH 操作、または sp_cursor SETPOSITION 操作が行われるまで有効なままになります。  
  
 SETPOSITION OR 句では、更新、更新、削除、またはロックが最後に変更された行にカーソルの位置を設定することによってリンクします。  
  
## <a name="rownum-parameter"></a>rownum パラメーター  
 指定した場合、 *rownum*パラメーターは、フェッチ バッファー内の行番号ではなくキーセット内の行番号として解釈できます。 コンカレンシー制御はユーザーが管理する必要があります。 したがって、SCROLL_LOCKS カーソルの場合はその行のロックを独自に保持し (トランザクションを使用できます)、 OPTIMISTIC カーソルの場合は、この操作を実行する前にその行をフェッチしておく必要があります。  
  
## <a name="table-parameter"></a>table パラメーター  
 場合、 *optype*値が UPDATE または INSERT、および完全更新または挿入ステートメントとして送信された、*値*パラメーターで指定された値*テーブル*は無視されます。  
  
> [!NOTE]  
>  ビューに関しては、ビューに参加している 1 つのテーブルを変更できます。 *値*パラメーターの列名は、ビュー内の列名を反映する必要がありますが、テーブル名には、(この場合 sp_cursor はの代わりにビュー名)、基になるベース テーブルの指定できます。  
  
## <a name="value-parameter"></a>パラメーターの値  
 規則を使用するために 2 つの代替案がない*値*「引数」セクションで述べた。  
  
1.  名前を使用することができます '\@' という名前のいずれかの選択リスト内の列の名前を付けた*値*パラメーター。 この方法には、データ変換が不要になる可能性があるという利点があります。  
  
2.  完全な UPDATE または INSERT ステートメントを送信するか、複数のパラメーターを使用して、完全なステートメントに SQL Server を作成し、UPDATE または INSERT ステートメントの一部を送信するには、パラメーターを使用します。 この例は、このトピックの「例」のセクションで確認できます。  
  
## <a name="examples"></a>使用例  
  
### <a name="alternative-value-parameter-uses"></a>パラメーターを使用して別の値  
 更新プログラム。  
  
 1 つのパラメーターを使用する場合、次の構文を使用して UPDATE ステートメントを送信できます。  
  
 `[ [ UPDATE <table name> ] SET ] {<column name> = expression} [,...n]`  
  
> [!NOTE]  
>  場合更新\<テーブル名 > を指定すると、任意の値がの指定、*テーブル*パラメーターは無視されます。  
  
 複数のパラメーターを使用している場合、最初のパラメーターは、次の形式の文字列である必要があります。  
  
 `[ SET ] <column name> = expression  [,...n]`  
  
 後続のパラメーターがの形式である必要があります。  
  
 `<column name> = expression  [,...n]`  
  
 ここで、\<テーブル名 > で作成される update ステートメントが指定した値または既定値に 1 つ、*テーブル*パラメーター。  
  
 挿入。  
  
 1 つのパラメーターを使用する場合は、次の構文を使用して INSERT ステートメントを送信できます。  
  
 `[ [ INSERT [INTO] <table name> ] VALUES ] ( <expression> [,...n] )`  
  
> [!NOTE]  
>  場合挿入 *\<テーブル名 >* を指定すると、任意の値がの指定、*テーブル*パラメーターは無視されます。  
  
 複数のパラメーターを使用している場合、最初のパラメーターは、次の形式の文字列である必要があります。  
  
 `[ VALUES ( ] <expression>  [,...n]`  
  
 後続のパラメーターがの形式である必要があります。  
  
 `expression [,...n]`  
  
 場所の値が指定されている場合があります、末尾を除く")"の後、最後の式。 ここで、 *\<テーブル名 >* で作成される UPDATE ステートメントが指定した値または既定値に 1 つ、*テーブル*パラメーター。  
  
> [!NOTE]  
>  1 つのパラメーターを名前付きパラメーターとして送信することもできます ("`@VALUES`" など)。 ここで使用することがあります他の名前付きパラメーターはありません。  
  
## <a name="see-also"></a>関連項目  
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
