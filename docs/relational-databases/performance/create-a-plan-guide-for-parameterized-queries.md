---
title: パラメーター化クエリのプラン ガイドの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- parameterized queries, plan guides for
- plan guides [SQL Server], parameterized queries
ms.assetid: b532ae16-66e7-4641-9bc8-b0d805853477
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 45a57f45eae2a54d73e08064b9a02446871f8400
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946956"
---
# <a name="create-a-plan-guide-for-parameterized-queries"></a>パラメーター化クエリのプラン ガイドの作成
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  TEMPLATE プラン ガイドでは、指定した形式にパラメーター化されたスタンドアロン クエリが照合されます。  
  
 次の例では、指定されたフォームにパラメーター化されるクエリに適合するプラン ガイドを作成し、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に対してクエリのパラメーター化を強制的に実行させます。 次の 2 つのクエリは構文的には同じですが、定数リテラル値のみが異なります。  
  
```  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45639;  
  
SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
    ON h.SalesOrderID = d.SalesOrderID  
WHERE h.SalesOrderID = 45640;  
```  
  
 パラメーター化形式のクエリに対するプラン ガイドは次のようになります。  
  
```  
EXEC sp_create_plan_guide   
    @name = N'TemplateGuide1',  
    @stmt = N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
              INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
                  ON h.SalesOrderID = d.SalesOrderID  
              WHERE h.SalesOrderID = @0',  
    @type = N'TEMPLATE',  
    @module_or_batch = NULL,  
    @params = N'@0 int',  
    @hints = N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
 この例では、 `@stmt` パラメーターの値は、パラメーター化形式のクエリになっています。 この値を取得して sp_create_plan_guide で使用できるようにするには、 [sp_get_query_template](../../relational-databases/system-stored-procedures/sp-get-query-template-transact-sql.md) システム ストアド プロシージャを使用するのが唯一信頼できる方法です。 次のスクリプトを使用すると、パラメーター化クエリを取得してそのクエリに対してプラン ガイドを作成することができます。  
  
```  
DECLARE @stmt nvarchar(max);  
DECLARE @params nvarchar(max);  
EXEC sp_get_query_template   
    N'SELECT * FROM AdventureWorks2012.Sales.SalesOrderHeader AS h  
      INNER JOIN AdventureWorks2012.Sales.SalesOrderDetail AS d   
          ON h.SalesOrderID = d.SalesOrderID  
      WHERE h.SalesOrderID = 45639;',  
    @stmt OUTPUT,   
    @params OUTPUT  
EXEC sp_create_plan_guide N'TemplateGuide1',   
    @stmt,   
    N'TEMPLATE',   
    NULL,   
    @params,   
    N'OPTION(PARAMETERIZATION FORCED)';  
```  
  
> [!IMPORTANT]  
>  `@stmt` に渡される `sp_get_query_template` パラメーターの定数リテラルの値は、リテラルを置き換えるパラメーターで選択されるデータ型に影響する場合があります。 この値は、プラン ガイドの適合にも影響します。 場合によっては、異なるパラメーター値範囲に対応する複数のプラン ガイドを作成する必要があります。  
  
 TEMPLATE プラン ガイドを SQL プラン ガイドと併用することもできます。 たとえば、TEMPLATE プラン ガイドを作成することで、特定のクラスのクエリについて確実にパラメーター化を行うことができます。 これにより、そのパラメーター化された形式のクエリに対して SQL プラン ガイドを作成できます。  
  
  
