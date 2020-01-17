---
title: transform noise words サーバー構成オプション | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- full-text queries [SQL Server], performance
- transform noise words option
- noise words [full-text search]
- full-text search [SQL Server], stopwords
- stopwords [full-text search]
ms.assetid: 69bd388e-a86c-4de4-b5d5-d093424d9c57
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6c5ddad15af74e45313d3e71b059fae36d166560
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62808693"
---
# <a name="transform-noise-words-server-configuration-option"></a>transform noise words サーバー構成オプション
  使用して、`transform noise words`サーバー構成オプションをエラー メッセージを抑制するかどうかノイズ ワード、つまり[ストップ ワード](../../relational-databases/search/full-text-search.md)、ゼロ行を返すフルテキスト クエリのブール演算が発生します。 フルテキスト クエリに使用されている CONTAINS 述語に、ノイズ ワードを含んだブール演算または NEAR 演算が存在する場合、このオプションを使用すると便利です。 次の表に、このオプションで使用可能な値を示します。  
  
|値|Description|  
|-----------|-----------------|  
|0|ノイズ ワード (ストップワード) は変換されません。 フルテキスト クエリにノイズ ワードが含まれている場合、クエリから返される行数は 0 件となり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] から警告が生成されます。 これは既定の動作です。<br /><br /> 警告は実行時の警告であることに注意してください。 そのため、クエリ内のフルテキスト句が実行されていない場合、警告は発生しません。 ローカル クエリの場合、複数のフルテキスト クエリ句がある場合でも、発生する警告は 1 つだけです。 リモート クエリの場合、リンク サーバーがエラーを中継しない場合があるので、警告が発生しないことがあります。|  
|1|ノイズ ワード (ストップワード) の変換が行われます。 これらは無視されて、残りのクエリが評価されます。<br /><br /> 近接語句内にノイズ ワードが指定された場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によって削除されます。 たとえば、ノイズ ワードである " `is` " は、 `CONTAINS(<column_name>, 'NEAR (hello,is,goodbye)')`から削除され、検索クエリは `CONTAINS(<column_name>, 'NEAR(hello,goodbye)')`に変換されます。 `CONTAINS(<column_name>, 'NEAR(hello,is)')` は、有効な検索用語が 1 つしか存在しないため、単純に `CONTAINS(<column_name>, hello)` に変換されます。|  
  
## <a name="effects-of-the-transform-noise-words-setting"></a>transform noise words 設定の影響  
 このセクションでは、ノイズ ワードである "`the`" を例に、`transform noise words` の設定によるクエリ動作の違いを見ていきます。  サンプルのフルテキスト クエリ文字列は、 `[1, "The black cat"]`というデータを含んだテーブル行に対して実行するものとします。  
  
> [!NOTE]  
>  このようなシナリオでは必ず、ノイズ ワードの警告が発生する可能性があります。  
  
-   transform noise words を 0 に設定した場合:  
  
    |クエリ文字列|結果|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|結果は返されません ("`the`" AND "`cat`" の場合も動作は同じ)。|  
    |"`cat`" NEAR "`the`"|結果は返されません ("`the`" NEAR "`cat`" の場合も動作は同じ)。|  
    |"`the`" AND NOT "`black`"|検索結果がありません|  
    |"`black`" AND NOT "`the`"|検索結果がありません|  
  
-   transform noise words を 1 に設定した場合:  
  
    |クエリ文字列|結果|  
    |------------------|------------|  
    |"`cat`" AND "`the`"|ID 1 の行がヒットします。|  
    |"`cat`" NEAR "`the`"|ID 1 の行がヒットします。|  
    |"`the`" AND NOT "`black`"|検索結果がありません|  
    |"`black`" AND NOT "`the`"|ID 1 の行がヒットします。|  
  
## <a name="example"></a>例  
 次の例では、`transform noise words` を `1` に設定します。  
  
```  
sp_configure 'show advanced options', 1;  
RECONFIGURE;  
GO  
sp_configure 'transform noise words', 1;  
RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>関連項目  
 [サーバー構成オプション &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [CONTAINS &#40;Transact-SQL&#41;](/sql/t-sql/queries/contains-transact-sql)  
  
  
