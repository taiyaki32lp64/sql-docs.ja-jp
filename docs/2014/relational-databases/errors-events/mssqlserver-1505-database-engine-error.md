---
title: MSSQLSERVER_1505 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1505 (Database Engine error)
ms.assetid: ef4df75d-0f36-4c8b-b36c-e427f65f91ca
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6ada58ff37b3fb7dd2760427483b0935d9bc47cb
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727741"
---
# <a name="mssqlserver1505"></a>MSSQLSERVER_1505
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|1505|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DUP_KEY|  
|メッセージ テキスト|オブジェクト名 '%.\*ls' およびインデックス名 '%.\*ls' の重複キーが見つかったため、CREATE UNIQUE INDEX が終了しました。  重複キーの値は %ls です。|  
  
## <a name="explanation"></a>説明  
 このエラーは、一意インデックスを作成しようとしたときに、指定した値がテーブルの 1 つ以上の行に含まれている場合に発生します。 一意インデックスは、インデックスを作成して UNIQUE キーワードを指定した場合、または UNIQUE 制約を作成した場合に作成されます。 インデックスまたは制約で定義された列の値が重複する行をテーブルに含めることはできません。  
  
 次の **Employee** テーブルのデータについて考えてみましょう。  
  
|LastName|FirstName|JobTitle|HireDate|  
|--------------|---------------|--------------|--------------|  
|Walters|Rob|上級ツール デザイナー|2004-11-19|  
|Brown|Kevin|マーケティング アシスタント|NULL|  
|Brown|Jo|デザイン エンジニア|NULL|  
|Walters|Rob|ツール デザイナー|2001-08-09|  
  
 **LastName** 列、または **LastName** 列と **FirstName** 列の組み合わせに対して一意インデックスを作成することはできません。これは行の値が重複しているためです。  
  
 よりわかりにくいのは、**HireDate** 列で一意性違反が発生する可能性があることです。 インデックスの作成という目的では、NULL 値は同じ値と見なされます。 したがって、複数行のキー値が NULL である場合は、一意インデックスまたは一意制約を作成できません。 上記のデータの場合、**HireDate** 列、または **LastName** 列と **HireDate** 列の組み合わせに対して一意インデックスを作成することはできません。  
  
 エラー メッセージ 1505 では、一意性制約に違反する最初の行が返されます。 これ以外にも重複行がテーブルに含まれている可能性があります。 重複行をすべて検出するには、指定されたテーブルに対してクエリを実行し、GROUP BY 句と HAVING 句を使用して重複行を抽出します。 たとえば、次のクエリを実行すると、姓と名が重複する **Employee** テーブル内の行が返されます。  
  
 SELECT LastName, FirstName, count(\*) FROM dbo.Employee GROUP BY LastName, FirstName HAVING count(\*) > 1;  
  
## <a name="user-action"></a>ユーザーの操作  
 次の解決策について検討してください。  
  
-   インデックス定義または制約定義の列を追加または削除し、一意の複合インデックスを作成します。 上記の例では、インデックス定義または制約定義に **MiddleName** 列を追加すると、重複に関する問題が解決される場合があります。  
  
-   一意インデックスまたは一意制約の列を選択する場合は、NOT NULL と定義された列を選択します。 これにより、複数の行のキー値に NULL が含まれている場合に発生する一意性違反の可能性がなくなります。  
  
-   重複値の原因がデータ エントリのエラーである場合は、そのデータを手動で修正してから、インデックスまたは制約を作成します。 テーブル内の重複行を削除する方法の詳細については、サポート技術情報の記事 139444「[テーブルから重複行を削除する方法](https://support.microsoft.com/kb/139444)」を参照してください。  
  
## <a name="see-also"></a>関連項目  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [Unique インデックスを作成します。](../indexes/indexes.md)   
 [UNIQUE 制約の作成](../tables/create-unique-constraints.md)  
  
  
