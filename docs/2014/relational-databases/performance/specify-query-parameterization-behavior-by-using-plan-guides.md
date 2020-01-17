---
title: プラン ガイドを使用したクエリのパラメーター化動作の指定 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- PARAMETERIZATION FORCED option
- PARAMETERIZATION option
- PARAMETERIZATION SIMPLE option
- parameterization [SQL Server]
- overriding parameterization behavior
- plan guides [SQL Server], parameterization
- parameterized queries [SQL Server]
ms.assetid: f0f738ff-2819-4675-a8c8-1eb6c210a7e6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: da60ceee93802b14b7d09392740a1f6b471e4ab1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150602"
---
# <a name="specify-query-parameterization-behavior-by-using-plan-guides"></a>プラン ガイドを使用したクエリのパラメーター化動作の指定
  PARAMETERIZATION データベース オプションが SIMPLE に設定されている場合、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] クエリ オプティマイザーはクエリのパラメーター化を選択することがあります。 これは、クエリに含まれるリテラル値がすべてパラメーターに置き換えられることを意味します。 この処理を簡易パラメーター化と呼びます。 簡易パラメーター化が有効であれば、クエリのパラメーター化を行う場合と行わない場合を制御することはできません。 ただし、PARAMETERIZATION データベース オプションを FORCED に設定することにより、データベース内のすべてのクエリをパラメーター化するように指定できます。 この処理を強制パラメーター化と呼びます。  
  
 次のような方法でプラン ガイドを使用すると、データベースのパラメーター化の動作をオーバーライドできます。  
  
-   PARAMETERIZATION データベース オプションが SIMPLE に設定されている場合、ある種のクエリについては強制パラメーター化を行うように指定できます。 これには、パラメーター化された形式のクエリの TEMPLATE プラン ガイドを作成し、 [sp_create_plan_guide](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) ストアド プロシージャに PARAMETERIZATION FORCED クエリ ヒントを指定します。 このようなプラン ガイドは、すべてのクエリではなく、ある種のクエリにのみパラメーター化を強制する方法と考えることができます。  
  
-   PARAMETERIZATION データベース オプションが FORCED に設定されている場合、ある種のクエリについては、強制パラメーター化ではなく簡易パラメーター化だけを行うように指定できます。 これには、強制パラメーター化された形式のクエリの TEMPLATE プラン ガイドを作成し、 **sp_create_plan_guide**に PARAMETERIZATION SIMPLE クエリ ヒントを指定します。  
  
 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースを対象とした次のクエリについて考えてみましょう。  
  
```  
SELECT pi.ProductID, SUM(pi.Quantity) AS Total  
FROM Production.ProductModel AS pm   
    INNER JOIN Production.ProductInventory AS pi   
        ON pm.ProductModelID = pi.ProductID   
WHERE pi.ProductID = 101   
GROUP BY pi.ProductID, pi.Quantity HAVING SUM(pi.Quantity) > 50;  
```  
  
 ここでは、データベース管理者が、データベースのすべてのクエリにパラメーター化を強制しないことに決定しました。 ただし、前のクエリと定数リテラル値だけが異なり、構文は同じクエリすべてにコンパイル コストが発生するのは避けたいと考えています。 つまり、クエリをパラメーター化し、この種のクエリのクエリ プランを再利用できるように考えています。 このような場合は、次の手順を実行します。  
  
1.  パラメーター化された形式のクエリを取得します。 **sp_create_plan_guide** で使用するためにこの値を安全に取得する唯一の方法は、 [sp_get_query_template](/sql/relational-databases/system-stored-procedures/sp-get-query-template-transact-sql) システム ストアド プロシージャを使う方法です。  
  
2.  パラメーター化された形式のクエリのプラン ガイドを作成し、PARAMETERIZATION FORCED クエリ ヒントを指定します。  
  
    > [!IMPORTANT]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] はクエリのパラメーター化処理の一環として、リテラルの値とサイズに従って、リテラル値を置き換えるパラメーターにデータ型を割り当てます。 **sp_get_query_template** の **@stmt** 出力パラメーターに定数リテラルの値が渡される場合も、これと同じ処理が行われます。 **sp_create_plan_guide** の **@params** 引数に指定されたデータ型は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] がパラメーター化を行う場合にクエリのデータ型と一致する必要があるので、クエリのパラメーター値としてとり得る値すべてに対応できるように、複数のプラン ガイドを作成しなければならない可能性があります。  
  
 次のスクリプトを使用すると、パラメーター化クエリの取得と、このクエリのプラン ガイドの作成の両方の処理を行えます。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT pi.ProductID, SUM(pi.Quantity) AS Total   
      FROM Production.ProductModel AS pm   
      INNER JOIN Production.ProductInventory AS pi ON pm.ProductModelID = pi.ProductID   
      WHERE pi.ProductID = 101   
      GROUP BY pi.ProductID, pi.Quantity   
      HAVING sum(pi.Quantity) > 50',  
    @stmt OUTPUT,   
    @params OUTPUT;  
EXEC sp_create_plan_guide   
    N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 同様に、強制パラメーター化が既に有効になっているデータベースでは、サンプルのクエリや、構文が同じでも定数リテラル値が異なるその他のクエリが、簡易パラメーター化のルールに従ってパラメーター化されるようにすることができます。 この場合は、OPTION 句に PARAMETERIZATION FORCED ではなく PARAMETERIZATION SIMPLE を指定します。  
  
> [!NOTE]  
>  TEMPLATE プラン ガイドは、ステートメントと、単一のステートメントのみで構成されるバッチにより送信されるクエリとを対応付けます。 複数のステートメントで構成されるバッチ内のステートメントは、TEMPLATE プラン ガイドで対応付けできません。  
  
  
