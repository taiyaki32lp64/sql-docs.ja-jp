---
title: メモリ最適化テーブルへの IDENTITY の実装 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: c0a704a3-3a31-4c2c-b967-addacda62ef8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 591d86011ee769d054c069db98a40e2765b1ec27
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63157820"
---
# <a name="implementing-identity-in-a-memory-optimized-table"></a>メモリ最適化テーブルへの IDENTITY の実装
  メモリ最適化テーブルでは、IDENTITY(1, 1) がサポートされています。 ただし、IDENTITY(x, y) という定義を持つ ID 列で、x != 1 または y != 1 の場合は、メモリ最適化テーブルでサポートされません。 シーケンス オブジェクトを使用する ID 値の回避策 ([シーケンス番号](../sequence-numbers/sequence-numbers.md))。  
  
 最初に、インメモリ OLTP に変換しているテーブルから IDENTITY プロパティを削除します。 次に、テーブルの列に新しい SEQUENCE オブジェクトを定義します。 SEQUENCE オブジェクトは IDENTITY 列として、新しい IDENTITY 値を取得する NEXT VALUE FOR 構文を使用する列の DEFAULT 値を作成する機能に依存します。 インメモリ OLTP では DEFAULT がサポートされていないため、新しく生成される SEQUENCE 値を INSERT 構文または挿入しないネイティブ コンパイル ストアド プロシージャに渡す必要があります。 次の例でそのパターンを示します。  
  
```sql  
-- Create a new In-Memory OLTP table to simulate IDENTITY insert  
-- Here the column C1 was the identity column in the original table  
--  
create table T1  
(  
  
[c1] integer not null primary key T1_c1 nonclustered,  
[c2] varchar(32) not null,  
[c3] datetime not null  
  
) with (memory_optimized = on)  
go  
  
-- This is a sequence provider that will give us values for column [c1]  
--  
create sequence usq_SequenceForT1 as integer start with 2 increment by 1  
go  
  
--   insert a sample row using the sequence  
--   note that a new value needs to be retrieved form   
--   the sequence object for every insert  
--  
declare @c1 integer = next value for [dbo].[usq_SequenceForT1]  
insert into T1 values (@c1, 'test', getdate())  
```  
  
 挿入を複数回実行した後、単調に増加する有効な値が列 [c1] に表示されます。 この結果セットは、`ORDER BY` を含まないテーブル スキャンとハッシュ インデックスを使用して生成されるため、行は順序付けされません。  
  
## <a name="see-also"></a>参照  
 [インメモリ OLTP への移行](migrating-to-in-memory-oltp.md)  
  
  
