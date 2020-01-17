---
title: SQLXML 4.0 での、アップデートグラムを使用したデータ変更
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- SQLXML, updategrams
- data insertions [SQLXML]
- data deletions [SQLXML]
- updating data [SQLXML]
- modifying data [SQLXML]
- OPENXML function
- updategrams [SQLXML]
- database modifications [SQLXML]
- data updates [SQLXML]
- modifying databases
- data modifications [SQLXML]
- deleting data
- inserting data
ms.assetid: b8b3b892-cb73-41d0-b945-bce148d81d9b
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 56a1d4b0243645c1d54b47145740f84fda29e841
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75247113"
---
# <a name="using-updategrams-to-modify-data-in-sqlxml-40"></a>SQLXML 4.0 での、アップデートグラムを使用したデータ変更
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  アップデートグラムまたは OPENXML [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../../includes/tsql-md.md)]関数を使用して、既存の XML ドキュメントからデータベースを変更 (挿入、更新、または削除) することができます。  
  
 ここでは、アップデートグラムについての情報と、その使用例を示します。  
  
## <a name="in-this-section"></a>このセクションの内容  
 [アップデートグラムの概要 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/introduction-to-updategrams-sqlxml-4-0.md)  
 アップデートグラムについての基本情報と使用例を示します。  
  
 [アップデートグラムでの注釈付きマッピングスキーマの指定 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/specifying-an-annotated-mapping-schema-in-an-updategram-sqlxml-4-0.md)  
 アップデートグラムの注釈付きマッピング スキーマについて説明し、使用例を示します。  
  
 [&#40;SQLXML 4.0&#41;の NULL 処理](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/null-handling-sqlxml-4-0.md)  
 要素値と属性値に NULL を指定する方法について説明します。  
  
 [XML アップデートグラムを使用したデータの挿入 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/inserting-data-using-xml-updategrams-sqlxml-4-0.md)  
 アップデートグラムを使用したデータの挿入について説明し、例を示します。  
  
 [XML アップデートグラムを使用したデータの削除 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/deleting-data-using-xml-updategrams-sqlxml-4-0.md)  
 アップデートグラムを使用したデータの削除について説明し、例を示します。  
  
 [XML アップデートグラムを使用したデータの更新 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/updating-data-using-xml-updategrams-sqlxml-4-0.md)  
 アップデートグラムを使用した既存データの変更について説明し、例を示します。  
  
 [アップデートグラムへのパラメーターの引き渡し &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/passing-parameters-to-updategrams-sqlxml-4-0.md)  
 アップデートグラムへのパラメーターの引き渡しについて説明し、例を示します。  
  
 [アップデートグラムでのデータベースの同時実行に関する問題の処理 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/handling-database-concurrency-issues-in-updategrams-sqlxml-4-0.md)  
 アップデートグラムでのコンカレンシーの問題に対応するために可能なさまざまなレベルの保護について説明し、例を示します。  
  
 [アップデートグラムサンプルアプリケーション &#40;SQLXML 4.0&#41;](https://msdn.microsoft.com/library/d2287e10-4007-4ba4-ad84-4e2b6adfede5)  
 アップデートグラムを使用したサンプル アプリケーションを提供します。  
  
 [XML アップデートグラムのガイドラインと制限 &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/updategrams/guidelines-and-limitations-of-xml-updategrams-sqlxml-4-0.md)  
 アップデートグラムを使用する場合の注意点をいくつか挙げます。  
  
  
