---
title: プラン ガイド | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- TEMPLATE plan guide
- SQL plan guides
- OPTIMIZE FOR query hint
- RECOMPILE query hint
- OBJECT plan guide
- plan guides [SQL Server], about plan guides
- OPTION clause
- plan guides [SQL Server]
- USE PLAN query hint
ms.assetid: bfc97632-c14c-4768-9dc5-a9c512f6b2bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ea11c177533a6101bb0654ca0450e85ea855d9a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150819"
---
# <a name="plan-guides"></a>プラン ガイド
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の実際のクエリのテキストを直接変更することが不可能な場合や望ましくない場合に、プラン ガイドを使用してクエリのパフォーマンスを最適化することができます。 プラン ガイドは、クエリ ヒントまたは固定クエリ プランをクエリにアタッチすることにより、クエリの最適化を促します。 プラン ガイドは、サード パーティ ベンダーが提供するデータベース アプリケーションのクエリの小さなサブセットで、期待どおりのパフォーマンスが得られない場合に役に立ちます。 プラン ガイドでは、最適化する Transact-SQL ステートメントのほか、使用するクエリ ヒントを含む OPTION 句またはクエリの最適化に使用する特定のクエリ プランのいずれかを指定します。 クエリが実行されると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により Transact-SQL ステートメントがプラン ガイドと照合され、実行時にクエリに OPTION 句がアタッチされるか、指定されたクエリ プランが使用されます。  
  
 作成できるプラン ガイドの総数の上限は、使用可能なシステム リソースによって決まります。 ただし、プラン ガイドは、ミッションクリティカルなクエリのパフォーマンスの向上と安定化を図る目的にのみ使用する必要があります。 プラン ガイドの使用により配置済みのアプリケーションのクエリ負荷の多くが影響を受けることがないようにしてください。  
  
> [!NOTE]  
>  プラン ガイドは、 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のすべてのエディションで使用できるわけではありません。 エディションでサポートされている機能の一覧については[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]を参照してください[機能は、SQL Server 2014 の各エディションでサポートされている](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)します。 プラン ガイドはどのエディションでも表示できます。 また、プラン ガイドを含むデータベースは、どのエディションに対してもアタッチできます。 アップグレード済みのバージョンの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]にデータベースを復元またはアタッチした場合、プラン ガイドはまったく影響を受けません。  
  
## <a name="types-of-plan-guides"></a>プラン ガイドの種類  
 次の種類のプラン ガイドを作成できます。  
  
 OBJECT プラン ガイド  
 OBJECT プラン ガイドでは、 [!INCLUDE[tsql](../../includes/tsql-md.md)] ストアド プロシージャ、スカラー ユーザー定義関数、複数ステートメント テーブル値ユーザー定義関数、および DML トリガーのコンテキストで実行されるクエリが照合されます。  
  
 `@Country`_`region` パラメーターを受け取る次のストアド プロシージャが、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに対して配置されたデータベース アプリケーションに存在するとします。  
  
```  
CREATE PROCEDURE Sales.GetSalesOrderByCountry (@Country_region nvarchar(60))  
AS  
BEGIN  
    SELECT *  
    FROM Sales.SalesOrderHeader AS h, Sales.Customer AS c,   
        Sales.SalesTerritory AS t  
    WHERE h.CustomerID = c.CustomerID  
        AND c.TerritoryID = t.TerritoryID  
        AND CountryRegionCode = @Country_region  
END;  
```  
  
 このストアド プロシージャは `@Country`_`region = N'AU'` (オーストラリア) 用にコンパイルおよび最適化されているものとします。 ただし、オーストラリアでは比較的少数の販売注文しか発生していないため、多くの販売注文が発生している国のパラメーター値を使用してクエリを実行するとパフォーマンスが低下します。 販売注文数が最も多いのは米国なので、 `@Country`\_`region = N'US'` 用に生成されたクエリ プランのパフォーマンスは、 `@Country`\_`region` パラメーターにどの値を使用しても低下しません。  
  
 ストアド プロシージャを変更して `OPTIMIZE FOR` クエリ ヒントをクエリに追加することで、この問題に対処できます。 ただし、ストアド プロシージャは配置済みアプリケーション内にあるので、アプリケーション コードを直接変更することはできません。 代わりに、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベースに次のプラン ガイドを作成できます。  
  
```  
sp_create_plan_guide   
@name = N'Guide1',  
@stmt = N'SELECT *FROM Sales.SalesOrderHeader AS h,  
        Sales.Customer AS c,  
        Sales.SalesTerritory AS t  
        WHERE h.CustomerID = c.CustomerID   
            AND c.TerritoryID = t.TerritoryID  
            AND CountryRegionCode = @Country_region',  
@type = N'OBJECT',  
@module_or_batch = N'Sales.GetSalesOrderByCountry',  
@params = NULL,  
@hints = N'OPTION (OPTIMIZE FOR (@Country_region = N''US''))';  
```  
  
 `sp_create_plan_guide` ステートメントの指定したクエリが実行されると、そのクエリは最適化される前に変更され、 `OPTIMIZE FOR (@Country = N''US'')` 句が含められます。  
  
 SQL プラン ガイド  
 SQL プラン ガイドでは、データベース オブジェクトの一部ではないスタンドアロン [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとスタンドアロン バッチのコンテキストで実行されるクエリが照合されます。 また、SQL ベースのプラン ガイドを使用して、指定した形式にパラメーター化されたクエリを照合することもできます。 SQL プラン ガイドは、スタンドアロン [!INCLUDE[tsql](../../includes/tsql-md.md)] ステートメントとスタンドアロン バッチに適用されます。 これらのステートメントは、よく [sp_executesql](/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql) システム ストアド プロシージャを使用してアプリケーションから送信されます。 たとえば、次のスタンドアロン バッチについて考えてみましょう。  
  
```  
SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC;  
```  
  
 このクエリに並列実行プランが生成されないようにするには、次のプラン ガイドを作成し、 `MAXDOP` パラメーターで `1` クエリ ヒントを `@hints` に設定します。  
  
```  
sp_create_plan_guide   
@name = N'Guide2',   
@stmt = N'SELECT TOP 1 * FROM Sales.SalesOrderHeader ORDER BY OrderDate DESC',  
@type = N'SQL',  
@module_or_batch = NULL,   
@params = NULL,   
@hints = N'OPTION (MAXDOP 1)';  
```  
  
> [!IMPORTANT]  
>  `@module_or_batch` ステートメントの `@params` 引数と `sp_create_plan guide` 引数に指定する値は、実際のクエリで送信される、対応するテキストと一致している必要があります。 詳細については、「 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql) ステートメントの [SQL Server Profiler を使用したプラン ガイドの作成とテスト](plan-guides.md)の実際のクエリのテキストを直接変更することが不可能な場合や望ましくない場合に、プラン ガイドを使用してクエリのパフォーマンスを最適化することができます。  
  
 PARAMETERIZATION データベース オプションを FORCED に設定するか、またはクエリのクラスをパラメーター化するように指定して TEMPLATE プラン ガイドを作成すると、同じ形式にパラメーター化されるクエリに SQL プラン ガイドを作成することもできます。  
  
 TEMPLATE プラン ガイド  
 TEMPLATE プラン ガイドでは、指定した形式にパラメーター化されたスタンドアロン クエリが照合されます。 これらのプラン ガイドは、クエリのクラスのデータベースの現在の PARAMETERIZATION データベース SET オプションをオーバーライドするために使用されます。  
  
 TEMPLATE プラン ガイドは、次のいずれかの状況で作成できます。  
  
-   PARAMETERIZATION データベース オプションを FORCED に設定したが、簡易パラメーター化のルールに従ってコンパイルするクエリがある場合。  
  
-   PARAMETERIZATION データベース オプションを SIMPLE (既定値) に設定したが、特定のクラスのクエリについて強制パラメーター化が必要である場合。  
  
## <a name="plan-guide-matching-requirements"></a>プラン ガイドの照合要件  
 プラン ガイドの範囲は、そのガイドが作成されているデータベースです。 したがって、クエリの実行時に使用されているデータベース内に存在するプラン ガイドだけをクエリと照合できます。 たとえば、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] が現在のデータベースの場合に次のクエリを実行するとします。  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 この場合、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] データベース内のプラン ガイドだけがこのクエリと照合されます。 ただし、 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] が現在のデータベースの場合に、次のステートメントを実行すると結果が異なります。  
  
 `USE DB1;`  
  
 `SELECT FirstName, LastName FROM Person.Person;`  
  
 この場合、 `DB1` のコンテキストでこのクエリが実行されているので、 `DB1`内のプラン ガイドがこのクエリと照合されます。  
  
 SQL ベースのプラン ガイドまたは TEMPLATE ベースのプラン ガイドでは、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] により、引数 @module_or_batch と引数 @params の値が文字単位で比較されてクエリと照合されます。 つまり、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で受け取られる実際のバッチ テキストと厳密に同じテキストを指定する必要があります。  
  
 @type = 'SQL' で、@module_or_batch が NULL に設定されている場合、@module_or_batch の値は @stmt の値に設定されます。つまり、 *statement_text* の値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]に送信するときと同一の形式で、同じ文字で指定する必要があります。 この適合を容易にするために内部変換は実行されません。  
  
 通常の (SQL または OBJECT) プラン ガイドと TEMPLATE プラン ガイドの両方をステートメントに適用可能な場合、通常のプラン ガイドのみが使用されます。  
  
> [!NOTE]  
>  プラン ガイドの作成対象のステートメントを含むバッチには、USE *database* ステートメントを含めることはできません。  
  
## <a name="plan-guide-effect-on-the-plan-cache"></a>プラン キャッシュに対するプラン ガイドの効果  
 モジュールにプラン ガイドを作成すると、そのモジュールのクエリ プランがプラン キャッシュから削除されます。 バッチに OBJECT 型または SQL 型のプラン ガイドを作成すると、同じハッシュ値を持つバッチのクエリ プランが削除されます。 TEMPLATE 型のプラン ガイドを作成すると、単一ステートメントのバッチがデータベース内のプラン キャッシュからすべて削除されます。  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|トピック|  
|----------|-----------|  
|プラン ガイドを作成する方法について説明します。|[新しいプラン ガイドの作成](create-a-new-plan-guide.md)|  
|パラメーター化クエリ用のプラン ガイドを作成する方法について説明します。|[パラメーター化クエリのプラン ガイドの作成](create-a-plan-guide-for-parameterized-queries.md)|  
|プラン ガイドを使用してクエリのパラメーター化動作を制御する方法について説明します。|[プラン ガイドを使用したクエリのパラメーター化動作の指定](specify-query-parameterization-behavior-by-using-plan-guides.md)|  
|プラン ガイドに固定クエリ プランを含める方法について説明します。|[プラン ガイドへの固定クエリ プランの適用](apply-a-fixed-query-plan-to-a-plan-guide.md)|  
|プラン ガイドにクエリ ヒントを指定する方法について説明します。|[プラン ガイドへのクエリ ヒントのアタッチ](attach-query-hints-to-a-plan-guide.md)|  
|プラン ガイドのプロパティを表示する方法について説明します。|[プラン ガイド プロパティの表示](view-plan-guide-properties.md)|  
|プラン ガイドを作成およびテストするために SQL Server Profiler を使用する方法について説明します。|[SQL Server Profiler を使用したプラン ガイドの作成とテスト](plan-guides.md)|  
|プラン ガイドを検証する方法について説明します。|[アップグレード後のプラン ガイドの検証](validate-plan-guides-after-upgrade.md)|  
  
## <a name="see-also"></a>関連項目  
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sp_control_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-control-plan-guide-transact-sql)   
 [sys.plan_guides &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-plan-guides-transact-sql)   
 [sys.fn_validate_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql)  
  
  
