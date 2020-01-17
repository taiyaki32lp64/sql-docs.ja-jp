---
title: sp_cursoropen (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoropen
- sp_cursoropen_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoropen
ms.assetid: 16462ede-4393-4293-a598-ca88c48ca70b
author: stevestein
ms.author: sstein
ms.openlocfilehash: f5127d041817a41dcf2d6fb4ed65070c87d05dd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108482"
---
# <a name="spcursoropen-transact-sql"></a>sp_cursoropen (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  カーソルを開きます。 sp_cursoropen は、カーソルやカーソル オプションに関連付けられている SQL ステートメントを定義し、カーソルを作成します。 sp_cursoropen の組み合わせに相当、[!INCLUDE[tsql](../../includes/tsql-md.md)]ステートメントの DECLARE_CURSOR と OPEN です。 この手順は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットでは 2 を = です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursoropen cursor OUTPUT, stmt  
    [, scrollopt[ OUTPUT ] [ , ccopt[ OUTPUT ]  
    [ ,rowcount OUTPUT [ ,boundparam][,...n]]] ]]  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 SQL Server で生成されたカーソル識別子。 *カーソル*は、*処理*値 sp_cursorfetch など、カーソルを使用するすべての後続プロシージャに渡す必要があります。 *カーソル*必須のパラメーターには、 **int**値を返します。  
  
 *カーソル*により、複数のカーソルを 1 つのデータベース接続でアクティブにします。  
  
 *stmt*  
 カーソル結果セットを定義する必須パラメーターです。 有効なクエリ文字列 (構文およびバインド) の任意の文字列型 (unicode、サイズなど) が有効なとして使用できる*stmt*値の型。  
  
 *scrollopt*  
 スクロール オプションです。 *scrollopt* 、省略可能なパラメーターが、次のいずれかを必要な**int**値を入力します。  
  
|値|説明|  
|-----------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
|0x10|FAST_FORWARD|  
|0x1000|PARAMETERIZED_STMT|  
|0x2000|AUTO_FETCH|  
|0x4000|AUTO_CLOSE|  
|0x8000|CHECK_ACCEPTED_TYPES|  
|0x10000|KEYSET_ACCEPTABLE|  
|0x20000|DYNAMIC_ACCEPTABLE|  
|0x40000|FORWARD_ONLY_ACCEPTABLE|  
|これに対して、0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 要求された値がによって定義されたカーソルの不適切である可能性*stmt*、このパラメーターは両方として機能入力し、出力します。 このような場合は、SQL Server によって適切な値が割り当てられます。  
  
 *ccopt*  
 同時実行制御オプションです。 *ccopt* 、省略可能なパラメーターが、次のいずれかを必要な**int**値を入力します。  
  
|[値]|説明|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (以前の LOCKCC)|  
|0x0004|**オプティミスティック**(以前の OPTCC)|  
|0x0008|OPTIMISTIC (以前の OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|これに対して、0x80000|OPTIMISITC_ACCEPTABLE|  
  
 同様*scrollopt*、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、要求されたをオーバーライドできます*ccopt*値。  
  
 *行数*  
 AUTO_FETCH で使用するフェッチ バッファー行の数。 既定値は、20 行です。 *rowcount*と戻り値の入力値として割り当てられている場合に異なる動作です。  
  
|入力値として|戻り値として|  
|--------------------|---------------------|  
|ときに、AUTO_FETCH *scrollopt*値が指定されて*rowcount*フェッチ バッファーに格納する行の数を表します。<br /><br /> 注: > 0 には有効な値がある場合、AUTO_FETCH が指定され、それ以外の場合は無視されます。|表します結果の行の数設定の場合を除き、 *scrollopt* AUTO_FETCH の値を指定します。|  
  
-  
  
 *boundparam*  
 追加のパラメーターの使用を示します。 *boundparam*場合に指定する省略可能なパラメーターです、 *scrollopt* PARAMETERIZED_STMT の値が ON に設定します。  
  
## <a name="return-code-values"></a>リターン コードの値  
 エラーが発生しなかった場合、sp_cursoropen は次のいずれかの値を返します。  
  
 0  
 正常に実行するプロシージャです。  
  
 0x0001  
 (軽度のエラー操作でエラーが発生する重大されません) の実行中にエラーが発生しました。  
  
 0x0002  
 非同期操作は実行中です。  
  
 0x0002  
 フェッチ操作は、処理中です。  
  
 A  
 このカーソルがによって割り当て解除されて[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]は使用できません。  
  
 エラーが発生したときに、戻り値が一致しない可能性があり、精度は保証できません。  
  
 ときに、 *rowcount*パラメーターは次の結果セットが発生した戻り値として指定します。  
  
 -1  
 行数が不明または適用外の場合に返されます。  
  
 -n  
 非同期設定が有効になっている場合に返されます。 フェッチに格納された行の数を表す場合にバッファー、 *scrollopt* AUTO_FETCH の値を指定します。  
  
 RPC が使用中の場合は、戻り値は次に示します。  
  
 0  
 プロシージャは成功します。  
  
 1  
 プロシージャが失敗しました。  
  
 2  
 キーセット カーソルが非同期に生成されています。  
  
 16  
 高速順方向カーソルが自動的に閉じられました。  
  
> [!NOTE]  
>  RPC がパラメーターと TDS の列の書式情報を含む結果セットを返す、sp_cursoropen プロシージャが正常に実行された場合 (0xa0 と 0xa1 メッセージ) 送信されます。 失敗した場合は、1 つまたは複数の TDS エラー メッセージが送信されます。 いずれの場合も、行のデータは返されません、*完了*メッセージ数が 0 になります。 バージョンを使用している場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]7.0 よりも前 0xa0 と 0xa1 (SELECT ステートメントの標準) が返されます 0xa5 および 0xa4 のトークン ストリームと共にします。 使用する場合[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]7.0 では、0x81、0xa5 および 0xa4 のトークン ストリームと共に (SELECT ステートメントの標準) が返されます。  
  
## <a name="remarks"></a>コメント  
  
## <a name="stmt-parameter"></a>stmt パラメーター  
 場合*stmt*実行を指定のストアド プロシージャでは、入力パラメーター可能性がありますかとして定義する定数の一部として、 *stmt*文字列、またはとして指定された*boundparam*引数。 宣言された変数は、この方法でバインドされたパラメーターとして渡すことができます。  
  
 許可されている内容、 *stmt*パラメーターによって異なるかどうか、 *ccopt* ALLOW_DIRECT がまたはの残りの部分に値がリンクされてを返す、 *ccopt*つまり、値します。  
  
-   ALLOW_DIRECT が指定されていない場合、いずれかを[!INCLUDE[tsql](../../includes/tsql-md.md)]SELECT ステートメントまたは EXECUTE ステートメントを呼び出す単一の SELECT ステートメントを含むストアド プロシージャを使用する必要があります。 さらに、SELECT ステートメントがカーソル; として修飾する必要があります。つまり、SELECT INTO または FOR BROWSE キーワードを含めることはできません。  
  
-   これが原因で、1 つまたは複数 ALLOW_DIRECT が指定されている場合[!INCLUDE[tsql](../../includes/tsql-md.md)]を含む複数のステートメントで他のストアド プロシージャを実行するステートメント。 SELECT 以外のステートメントまたはキーワード SELECT INTO または FOR BROWSE を含む SELECT ステートメントは、単純に実行して、カーソルは作成されません。 複数のステートメントのバッチに含まれている SELECT ステートメントについても同様です。 SELECT ステートメントがカーソルのみに関連する句が含まれている場合、それらの句は無視されます。 たとえばの値*ccopt*が 0x2002 の場合、これは、要求。  
  
    -   スクロール ロックを使用するカーソル (カーソルの条件を満たしている単一の SELECT ステートメントだけがある場合)。  
  
    -   複数のステートメント、SELECT 以外の 1 つのステートメントまたはカーソルとして扱われませんを SELECT ステートメントがある場合のステートメントの直接実行します。  
  
## <a name="scrollopt-parameter"></a>scrollopt パラメーター  
 最初の 5 つ*scrollopt*値 (KEYSEY、DYNAMIC、FORWARD_ONLY、STATIC、および FAST_FORWARD) は相互に排他的です。  
  
 PARAMETERIZED_STMT と CHECK_ACCEPTED_TYPES はまたはの最初の 5 つの値にリンクできます。  
  
 AUTO_FETCH と AUTO_CLOSE は、fast_forward またはをリンクできます。  
  
 CHECK_ACCEPTED_TYPES が ON の直前の 5 つの少なくとも 1 つ場合*scrollopt*値 (KEYSET_ACCEPTABLE`,` DYNAMIC_ACCEPTABLE、FORWARD_ONLY_ACCEPTABLE、STATIC_ACCEPTABLE、または FAST_FORWARD_ACCEPTABLE) である必要があります。  
  
 静的カーソルは常に READ_ONLY として開かれます。 したがって、このカーソルを使用して基になるテーブルを更新することはできません。  
  
## <a name="ccopt-parameter"></a>ccopt パラメーター  
 最初の 4 つ*ccopt*値 (READ_ONLY、SCROLL_LOCKS、および両方の OPTIMISTIC 値) は相互に排他的です。  
  
> [!NOTE]  
>  最初の 4 つのいずれかを選択する*ccopt*かどうか、カーソルが読み取り専用、または更新データの喪失を防ぐために、ロックやオプティミスティックの方法が使用されるかどうかに値が決まります。 場合、 *ccopt*値が指定されていない、既定値は OPTIMISTIC です。  
  
 ALLOW_DIRECT と CHECK_ACCEPTED_TYPES はまたはの最初の 4 つの値にリンクできます。  
  
 によって、または READ_ONLY、SCROLL_LOCKS、またはそのいずれかの OPTIMISTIC 値には、UPDT_IN_PLACE をリンクすることができます。  
  
 CHECK_ACCEPTED_TYPES が ON の最後の 4 つの少なくとも 1 つ場合*ccopt*値 (READ_ONLY_ACCEPTABLE、SCROLL_LOCKS_ACCEPTABLE、およびそのいずれかの OPTIMISTIC_ACCEPTABLE 値) にある必要があります。  
  
 位置指定更新と削除関数を場合にのみ、フェッチ バッファー内でのみ実行可能性があります、 *ccopt*値が SCROLL_LOCKS または OPTIMISTIC です。 SCROLL_LOCKS が指定された値の場合、操作が成功する保証します。 OPTIMISTIC が指定された値の場合は、最後にフェッチしたため、行が変更された場合、操作は失敗します。  
  
 指定されている値が OPTIMISTIC の場合に操作が失敗することがあるのは、タイムスタンプかチェックサム値 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって決定されます) を比較することによってオプティミスティック同時実行制御機能が実行されるためです。 一致しない行があると操作が失敗します。  
  
 戻り値として UPDT_IN_PLACE を指定することは、次の結果を制御します。  
  
-   存在しない場合、カーソルの一意のインデックスを持つテーブルで位置指定更新を実行するときにセット作業テーブルから行を削除します。 これらの列が変更され、カーソルで使用されるキー列のいずれかの末尾に挿入します。  
  
-   かどうか設定と、カーソルだけが更新されます、作業テーブルの元の行のキー列。  
  
## <a name="boundparam-parameter"></a>bound_param パラメーター  
 パラメーター名を指定する必要があります*paramdef*コード内のエラー メッセージに従って PARAMETERIZED_STMT が指定するとします。 PARAMETERIZED_STMT が指定されていない場合は、エラー メッセージに名前は指定されません。  
  
## <a name="rpc-considerations"></a>RPC に関する考慮事項  
 RPC の RETURN_METADATA 入力フラグを 0x0001 に設定すると、そのカーソル選択リストのメタデータを TDS ストリームで返すように要求します。  
  
## <a name="examples"></a>使用例  
  
### <a name="boundparam-parameter"></a>bound_param パラメーター  
 5 番目より後のパラメーターは、入力パラメーターとしてステートメント プランにに沿って渡されます。 最初にそのようなパラメーターがの形式で文字列をする必要があります。  
  
 *{0} データ型のローカル変数名}[,...n]*  
  
 代わりに使用する値を渡すための後続のパラメーターに使用、*ローカル変数の名前*ステートメントでします。  
  
## <a name="see-also"></a>関連項目  
 [sp_cursorfetch &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
