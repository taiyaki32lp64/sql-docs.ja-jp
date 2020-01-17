---
title: FOR XML AUTO クエリが互換性モード 90 以上で派生テーブル参照を返します |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- FOR XML AUTO [SQL Server]
ms.assetid: 10c32f06-f7e1-40e0-8f79-6d921f2bef1d
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5b42d8fd7694aaa3962d049cb0e9663479778958
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095189"
---
# <a name="for-xml-auto-queries-return-derived-table-references-in-90-or-later-compatibility-modes"></a>互換性モード 90 以上では FOR XML AUTO クエリが派生テーブルの参照を返す
  データベースの互換性レベルが 90 以上に設定されている場合、AUTO モードで実行する FOR XML クエリは派生テーブルの別名への参照を返します。 互換性レベルが 80 に設定されている場合、FOR XML AUTO クエリは派生テーブルを定義するベース テーブルへの参照を返します。  
  
## <a name="component"></a>コンポーネント  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>説明  
 たとえば、次のテーブルについて考えてみます。  
  
```  
CREATE TABLE Test(id int);  
INSERT INTO Test VALUES(1);  
INSERT INTO Test VALUES(2);  
```  
  
 次のクエリには派生テーブルが含まれており、互換性レベル 80 と 90 以上では異なる結果が生成されます。  
  
```  
SELECT * FROM   
   (SELECT a.id AS a, b.id AS b   
    FROM Test a JOIN Test b ON a.id=b.id)  
AS DerivedTest   
FOR XML AUTO;  
```  
  
 互換性レベル 80 では、クエリは次の結果を返します。 この結果は、派生テーブルの別名ではなく、派生テーブルのベース テーブルの別名 `a` と `b` を参照しています。  
  
```  
<a a="1"><b b="1"/></a><a a="2"><b b="2"/></a>  
```  
  
 互換性レベル 90 以上では、クエリは派生テーブルのベース テーブルへの参照ではなく、派生テーブルの別名 `DerivedTest` への参照を返します。  
  
```  
<DerivedTest a="1" b="1"/><DerivedTest a="2" b="2"/>  
```  
  
## <a name="corrective-action"></a>修正措置  
 派生テーブルを含んでいる FOR XML AUTO クエリのうち、互換性レベル 90 以上で実行されるクエリの結果が変化している場合、必要に応じてアプリケーションを修正してください。  
  
## <a name="see-also"></a>参照  
 [データベース エンジンのアップグレードに関する問題](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 アップグレード アドバイザー&#91;新規&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
