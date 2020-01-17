---
title: sp_cursoroption (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursoroption_TSQL
- sp_cursoroption
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursoroption
ms.assetid: 88fc1dba-f4cb-47c0-92c2-bf398f4a382e
author: stevestein
ms.author: sstein
ms.openlocfilehash: dce66e74f7415a8ff5ac6de4505d8a1f0632391b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68108454"
---
# <a name="spcursoroption-transact-sql"></a>sp_cursoroption (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  カーソル オプションを設定するか、sp_cursoropen ストアド プロシージャによって作成されたカーソル情報を返します。 sp_cursoroption は、ID を指定して呼び出される、表形式データ ストリーム (TDS) パケットで 8 を = です。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursoroption cursor, code, value  
```  
  
## <a name="arguments"></a>引数  
 *cursor*  
 *処理*によって生成される値[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sp_cursoropen ストアド プロシージャによって返されるとします。 *カーソル*が必要です、 **int**実行用の値を入力します。  
  
 *code*  
 カーソル戻り値のさまざまな要因を指定するために使用されます。 *コード*、次のいずれかが必要です**int**値を入力します。  
  
|[値]|名前|説明|  
|-----------|----------|-----------------|  
|0x0001|TEXTPTR_ONLY|指定された特定の text 列または image 列の実際のデータではなくテキスト ポインターを返します。<br /><br /> Textptr_only として使用するテキスト ポインター*ハンドル*選択的に取得できるは後を使用して更新または blob オブジェクトに[!INCLUDE[tsql](../../includes/tsql-md.md)]または DBLIB 機能 (例。[!INCLUDE[tsql](../../includes/tsql-md.md)] READTEXT や DBLIB dbwritetext など)。<br /><br /> 値 0 が割り当てられている場合は、選択リスト内のすべての text 列および image 列がデータではなくテキスト ポインターを返します。|  
|0x0002|CURSOR_NAME|指定された名前を割り当てます*値*カーソルにします。 ODBC を使用する、これにより、さらに、 [!INCLUDE[tsql](../../includes/tsql-md.md)] UPDATE または DELETE ステートメントを sp_cursoropen によって開かれるカーソルに配置されています。<br /><br /> 文字列は、任意の文字または Unicode データ型として指定できます。<br /><br /> [!INCLUDE[tsql](../../includes/tsql-md.md)]位置指定更新/削除ステートメント機能、既定でファット カーソルの場合の最初の行に対して sp_cursor SETPOSITION を位置指定の UPDATE または DELETE ステートメントを発行する前にカーソルを使用する必要があります。|  
|0x0003|TEXTDATA|以降のフェッチで、特定の text 列または image 列のテキスト ポインターではなく実際のデータを返します (これにより、TEXTPTR_ONLY の効力が取り消されます)。<br /><br /> 特定の列で TEXTDATA が有効になると、行は再フェッチ (更新) されます。後で TEXTPTR_ONLY に戻すことができます。 TEXTPTR_ONLY と同様に、value パラメーターは列番号を指定する整数で、値が 0 の場合はすべての text 列および image 列が返されます。|  
|0x0004|SCROLLOPT|スクロール オプションです。 詳細については、このトピックの後半では、「コードに返される値」を参照してください。|  
|0x0005|CCOPT|同時実行制御オプションです。 詳細については、このトピックの後半では、「コードに返される値」を参照してください。|  
|0x0006|ROWCOUNT|結果セットの現在の行の数。<br /><br /> 注:行カウントは、非同期設定が使用されている場合は、sp_cursoropen から返される値以降に変更された可能性があります。 行の数が不明の場合、値-1 が返されます。|  
  
 *value*  
 によって返される値を指定*コード*します。 *値*0x0001、0x0002、または 0x0003 を呼び出して取得する必須パラメーター*コード*値を入力します。  
  
> [!NOTE]  
>  A*コード*2 の値が文字列データ型。 その他の*コード*値を入力するかによって返される*値*は整数です。  
  
## <a name="return-code-values"></a>リターン コードの値  
 *値*パラメーターは、次のいずれかを返す可能性があります*コード*値。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0004|SCROLLOPT|  
|0X0005|CCOPT|  
|0X0006|ROWCOUNT|  
  
 *値*パラメーターは、次の SCROLLOPT 値のいずれかを返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0001|KEYSET|  
|0x0002|DYNAMIC|  
|0x0004|FORWARD_ONLY|  
|0x0008|STATIC|  
  
 *値*パラメーターは、次の CCOPT 値のいずれかを返します。  
  
|戻り値|説明|  
|------------------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS|  
|0x0004 または 0x0008|OPTIMISTIC|  
  
## <a name="see-also"></a>関連項目  
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cursor &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursor-transact-sql.md)   
 [sp_cursoropen &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)  
  
  
