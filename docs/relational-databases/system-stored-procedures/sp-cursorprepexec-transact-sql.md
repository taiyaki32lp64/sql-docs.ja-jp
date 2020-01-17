---
title: sp_cursorprepexec (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 08/20/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cursorprepexec_TSQL
- sp_cursorprepexec
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cursorprepexec
ms.assetid: 8094fa90-35b5-4cf4-8012-0570cb2ba1e6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 660a75f1e6fea9b5a825372501c2e65f2dd3874b
ms.sourcegitcommit: 5e838bdf705136f34d4d8b622740b0e643cb8d96
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/20/2019
ms.locfileid: "69652436"
---
# <a name="sp_cursorprepexec-transact-sql"></a>sp_cursorprepexec (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  送信されたカーソルステートメントまたはバッチのプランをコンパイルし、カーソルを作成して設定します。 sp_cursorprepexec は、sp_cursorprepare と sp_cursorexecute の関数を組み合わせたものです。 このプロシージャは、ID = 5 を指定した場合に表形式のデータストリーム (TDS) パケットで呼び出されます。  
  
 ![リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
sp_cursorprepexec prepared handle OUTPUT, cursor OUTPUT, params , statement , options  
    [ , scrollopt [ , ccopt [ , rowcount ] ] ]  
    [, '@parameter_name[,...n ]']
```  
  
## <a name="arguments"></a>引数  
 *準備済みハンドル*  
 は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成される準備済み*ハンドル*識別子です。 *準備*されたハンドルが必要です。 **int**を返します。  
  
 *cursor*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]生成されたカーソル識別子です。 *cursor*は必須パラメーターであり、このカーソルに対して操作する後続のすべてのプロシージャ (たとえば、sp_cursorfetch) で指定する必要があります。  
  
 *params*  
 パラメーター化されたステートメントを指定します。 変数の*params*定義は、ステートメントのパラメーターマーカーに置き換えられます。 *params*は、 **ntext**、 **nchar**、または**nvarchar**の入力値を呼び出す必須のパラメーターです。  
  
> [!NOTE]  
>  *Stmt*がパラメーター化され、 *scrollopt* PARAMETERIZED_STMT 値が ON の場合、入力値として**ntext**文字列を使用します。  
  
 *statement*  
 カーソル結果セットを定義します。 *ステートメント*のパラメーターは必須であり、 **ntext**、 **nchar**、または**nvarchar**の入力値に対してを呼び出します。  
  
> [!NOTE]  
>  Stmt の値を指定するためのルールは、sp_cursoropen の場合と同じですが、 *stmt*文字列のデータ型は**ntext**である必要があります。  
  
 *options*  
 カーソル結果セット列の説明を返す省略可能なパラメーターです。 \* オプションには、次の**int**入力値が必要です。  
  
|値|説明|  
|-----------|-----------------|  
|0x0001|RETURN_METADATA|  
  
 *scrollopt*  
 スクロールオプション。 *scrollopt*は省略可能なパラメーターで、次のいずれかの**int**入力値を必要とします。  
  
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
|0x80000|STATIC_ACCEPTABLE|  
|0x100000|FAST_FORWARD_ACCEPTABLE|  
  
 要求されたオプションが *\<stmt >* によって定義されたカーソルに適していない可能性があるため、このパラメーターは入力と出力の両方として機能します。 このような場合は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって適切な型が割り当てられ、この値が変更されます。  
  
 *ccopt*  
 同時実行制御オプション。 *ccopt*は省略可能なパラメーターで、次のいずれかの**int**入力値を必要とします。  
  
|値|説明|  
|-----------|-----------------|  
|0x0001|READ_ONLY|  
|0x0002|SCROLL_LOCKS (以前の LOCKCC)|  
|0x0004|**オプティミスティック**(以前は OPTCC と呼ばれていました)|  
|0x0008|オプティミスティック (以前の OPTCCVAL)|  
|0x2000|ALLOW_DIRECT|  
|0x4000|UPDT_IN_PLACE|  
|0x8000|CHECK_ACCEPTED_OPTS|  
|0x10000|READ_ONLY_ACCEPTABLE|  
|0x20000|SCROLL_LOCKS_ACCEPTABLE|  
|0x40000|OPTIMISTIC_ACCEPTABLE|  
|0x80000|OPTIMISITC_ACCEPTABLE|  
  
 *同様 scrollpt,* と同様に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 、は要求された値とは異なる値を割り当てることができます。  
  
 *行*  
 は、AUTO_FETCH で使用するフェッチバッファー行の数を示す省略可能なパラメーターです。 既定値は20行です。 *rowcount*の動作は、入力値と戻り値として割り当てられた場合に異なります。  
  
|入力値として|戻り値として|  
|--------------------|---------------------|  
|AUTO_FETCH が FAST_FORWARD cursor と共に指定されている場合、 *rowcount*はフェッチバッファーに格納する行の数を表します。|結果セット内の行の数を表します。 *Scrollopt* AUTO_FETCH 値を指定すると、 *rowcount*はフェッチバッファーにフェッチされた行の数を返します。|  

*parameter_name*Params 引数で定義されている1つ以上のパラメーター名を指定します。  Params に含まれるすべてのパラメーターにパラメーターが指定されている必要があります。 この引数は、Transact-sql ステートメントまたはバッチ内のバッチにパラメーターが定義されていない場合は必要ありません。
  
## <a name="return-code-values"></a>リターン コードの値  
 Params が NULL 値を返す場合、ステートメントはパラメーター化されません。  
  
## <a name="see-also"></a>関連項目  
 [sp_cursoropen &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursoropen-transact-sql.md)   
 [sp_cursorexecute &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorexecute-transact-sql.md)   
 [sp_cursorprepare &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorprepare-transact-sql.md)   
 [sp_cursorfetch &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-cursorfetch-transact-sql.md)   
 [システム ストアド プロシージャ &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
