---
title: TEXTVALID (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- TEXTVALID_TSQL
- TEXTVALID
dev_langs:
- TSQL
helpviewer_keywords:
- invalid text pointers [SQL Server]
- valid text pointers [SQL Server]
- TEXTVALID function
- checking text pointers
- text-pointer values
- verifying text pointers
ms.assetid: 9411c349-b59b-4740-a270-92f91d81ad23
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0608d1c5bd8c24fc9e78b21abf7cad6b1045db18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68099037"
---
# <a name="text-and-image-functions---textvalid-transact-sql"></a>テキスト関数とイメージ関数 - TEXTVALID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  特定のテキスト ポインターが有効であるかどうかを確認する、**text**、**ntext**、または **image** 型の関数です。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]代替機能を使用することはできません。  
  
 ![トピック リンク アイコン](../../database-engine/configure-windows/media/topic-link.gif "トピック リンク アイコン") [Transact-SQL 構文表記規則](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>構文  
  
```  
  
TEXTVALID ( 'table.column' ,text_ ptr )  
```  
  
## <a name="arguments"></a>引数  
 *テーブル*  
 使用するテーブルの名前です。  
  
 *column*  
 使用する列の名前です。  
  
 *text_ptr*  
 確認するテキスト ポインターです。  
  
## <a name="return-types"></a>戻り値の型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 ポインターが有効なら 1 を、ポインターが無効なら 0 を返します。 **text** 列の識別子には、テーブル名を含む必要があることに注意してください。 有効なテキスト ポインターがないと、UPDATETEXT、WRITETEXT、READTEXT は使用できません。  
  
 次の関数とステートメントは、**text**、**ntext**、および **image** データを操作する場合にも役立ちます。  
  
|関数またはステートメント|[説明]|  
|---------------------------|-----------------|  
|PATINDEX **(** ' _%pattern%_ ' **,** _expression_ **)**|**text** および **ntext** 列で指定された文字列の文字位置を返します。|  
|DATALENGTH **(** _expression_ **)**|**text**、**ntext**、**image** 列のデータの長さを返します。|  
|[SET TEXTSIZE]|SELECT ステートメントで返される **text**、**ntext**、または **image** データの制限値をバイト単位で返します。|  
  
## <a name="examples"></a>使用例  
 次の例では、`logo` テーブルの `pub_info` 列の各値に対して、有効なテキスト ポインターが存在するかどうかを報告します。  
  
> [!NOTE]  
>  この例を実行するには、**pubs** データベースをインストールする必要があります。  
  
```  
USE pubs;  
GO  
SELECT pub_id, 'Valid (if 1) Text data'   
   = TEXTVALID ('pub_info.logo', TEXTPTR(logo))   
FROM pub_info  
ORDER BY pub_id;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
pub_id Valid (if 1) Text data   
------ ----------------------   
0736   1                        
0877   1                        
1389   1                        
1622   1                        
1756   1                        
9901   1                        
9952   1                        
9999   1                        
  
(8 row(s) affected)  
```  
  
## <a name="see-also"></a>参照  
 [DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)   
 [PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)   
 [SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)   
 [テキスト関数とイメージ関数 &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)   
 [TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)  
  
  
