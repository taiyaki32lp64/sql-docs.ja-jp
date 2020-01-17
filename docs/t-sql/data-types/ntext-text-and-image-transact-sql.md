---
title: ntext、text、および image (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ntext_TSQL
- ntext
dev_langs:
- TSQL
helpviewer_keywords:
- text data type, about text data type
- text [SQL Server], data types
- ntext data type
- ntext data type, about ntext data type
- image data type, about image data type
ms.assetid: b0d8769c-7598-4f97-8162-ace5f182b5bc
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8aaae44a73bc7cd7ccf41bf1c33823664044a2e1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086734"
---
# <a name="ntext-text-and-image-transact-sql"></a>ntext、text、および image (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

大きな非 Unicode 文字および Unicode 文字とバイナリ データを格納するための固定長および可変長のデータ型。 Unicode データでは UNICODE UCS-2 文字セットが使用されます。
  
>**重要:**  **ntext**、**text**、および **image** データ型は、今後のバージョンの SQL Server で削除される予定です。 新しい開発作業では、これらのデータ型の使用は避け、現在これらのデータ型を使用しているアプリケーションは修正するようにしてください。 代わりに、 [nvarchar(max)](../../t-sql/data-types/nchar-and-nvarchar-transact-sql.md)、 [varchar(max)](../../t-sql/data-types/char-and-varchar-transact-sql.md)、 [varbinary(max)](../../t-sql/data-types/binary-and-varbinary-transact-sql.md) を使用してください。  
  
  
## <a name="arguments"></a>引数  
**ntext**  
文字列の最大長が 2^30 - 1 (1,073,741,823) の可変長の Unicode データを指定します。 ストレージ サイズは、入力する文字列長の 2 倍のバイト長です。 ISO シノニムは、 **ntext** は **national text**です。
  
**text**  
サーバーのコード ページ内の可変長の非 Unicode データを指定します。最大文字列長は 2^31-1 (2,147,483,647) 文字です。 サーバー コード ページで 2 バイト文字が使用されている場合、ストレージのサイズは 2,147,483,647 バイトのままです。 文字列によっては、格納サイズが 2,147,483,647 バイトより少なくなることもあります。
  
**image**  
0 ～ 2^31-1 (2,147,483,647) バイトの可変長のバイナリ データを指定します。
  
## <a name="remarks"></a>Remarks  
次の関数とステートメントで使用できる **ntext**, 、**テキスト**, 、または **イメージ** データ。
  
|関数|ステートメント|  
|---|---|
|[DATALENGTH &#40;Transact-SQL&#41;](../../t-sql/functions/datalength-transact-sql.md)|[READTEXT &#40;Transact-SQL&#41;](../../t-sql/queries/readtext-transact-sql.md)|  
|[PATINDEX &#40;Transact-SQL&#41;](../../t-sql/functions/patindex-transact-sql.md)|[SET TEXTSIZE &#40;Transact-SQL&#41;](../../t-sql/statements/set-textsize-transact-sql.md)|  
|[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)|[UPDATETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/updatetext-transact-sql.md)|  
|[TEXTPTR &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textptr-transact-sql.md)|[WRITETEXT &#40;Transact-SQL&#41;](../../t-sql/queries/writetext-transact-sql.md)|  
|[TEXTVALID &#40;Transact-SQL&#41;](../../t-sql/functions/text-and-image-functions-textvalid-transact-sql.md)||  
  
## <a name="see-also"></a>参照
[CAST および CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[データ型の変換 &#40;データベース エンジン&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[データ型 &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[照合順序と Unicode のサポート](../../relational-databases/collations/collation-and-unicode-support.md)

