---
title: アップグレード後は、新しい予約済みキーワードを識別子として使用できません |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- keywords [SQL Server], after upgrade
- keywords [SQL Server], reserved
- keywords [SQL Server]
ms.assetid: cb242081-54f8-4273-a8ef-52f3751c25ef
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8db9bcef48b28594187aab34fb0049689d907a47
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2018
ms.locfileid: "53376234"
---
# <a name="after-upgrade-new-reserved-keywords-cannot-be-used-as-identifiers"></a>アップグレード後に、予約された新しいキーワードを識別子として使用できない
  アップグレード アドバイザーは、予約されたキーワードとして使用されている単語を検出しました。 予約されたキーワードは、名前を区切らない限り、識別子またはオブジェクトの名前として使用することはできません。  
  
## <a name="component"></a>コンポーネント  
 データベース エンジン  
  
## <a name="description"></a>説明  
 互換性レベル 90 以下では、次の単語は予約されたキーワードではなく、[!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプト内で識別子またはオブジェクトの名前として使用できます。 互換性レベル 100 では、これらの単語は完全に予約されたキーワードで、識別子またはオブジェクトの名前として使用できません。  
  
-   EXTERNAL  
  
-   MERGE  
  
-   PIVOT  
  
-   REVERT  
  
-   STOPLIST  
  
-   TABLESAMPLE  
  
-   UNPIVOT  
  
## <a name="corrective-action"></a>修正措置  
 オブジェクトの名前を変更することをお勧めします。 アップグレードの前にオブジェクトの名前を変更できない場合は、名前を変更できるまで、次のいずれかの方法を使用してください。  
  
-   データベース互換性レベルの設定を 90 以下に保持します。  
  
-   区切られた識別子を使用して、オブジェクトを参照します。 たとえば、ステートメント`CREATE TABLE [MERGE] ([MERGE] int);`をオブジェクト名 MERGE を区切るために角かっこを使用します。  
  
## <a name="external-resources"></a>外部リソース  
 [予約済みキーワード&#40;TRANSACT-SQL&#41;](/sql/t-sql/language-elements/reserved-keywords-transact-sql)  
  
 [MERGE &#40;Transact-SQL&#41;](/sql/t-sql/statements/merge-transact-sql)  
  
 [区切られた識別子 (データベース エンジン)](https://go.microsoft.com/fwlink/?LinkId=112509)  
  
 [ALTER DATABASE 互換性レベル &#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level)  
  
  
