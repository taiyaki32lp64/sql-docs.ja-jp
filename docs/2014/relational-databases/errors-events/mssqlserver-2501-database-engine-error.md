---
title: MSSQLSERVER_2501 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2501 (Database Engine error)
ms.assetid: 895aafe3-a4e7-4ed8-acc5-93be76ef3664
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d4920be6af560cbd5bd1d7699dd6378cdc2db3b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62914852"
---
# <a name="mssqlserver2501"></a>MSSQLSERVER_2501
    
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|製品名|SQL Server|  
|イベント ID|2501|  
|イベント ソース|MSSQLSERVER|  
|コンポーネント|SQLEngine|  
|シンボル名|DBCC_NO_SUCH_TABLE_NAME|  
|メッセージ テキスト|'NAME' という名前のテーブルまたはオブジェクトが見つかりません。 システム カタログを確認してください。|  
  
## <a name="explanation"></a>説明  
 指定されたオブジェクトが見つかりません。  
  
### <a name="possible-causes"></a>考えられる原因  
 このエラーは次のいずれかの問題が原因で生じている可能性があります。  
  
-   オブジェクトが正しく指定されていない。  
  
-   オブジェクトが存在しないか、ステートメントが使用しようとする前に削除された。  
  
-   オブジェクトは存在するが、ユーザーからアクセスできない。 たとえば、オブジェクトに対する権限がユーザーにない場合や、オブジェクトがユーザーからは見えない内部テーブルである場合などが考えられます。  
  
## <a name="user-action"></a>ユーザーの操作  
  
-   現在のデータベース コンテキストが正しいことを確認します。 詳細については、「[USE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/use-transact-sql)」を参照してください。  
  
-   テーブルまたはオブジェクトの名前が正しく入力されていることを確認します。  
  
-   オブジェクトが含まれているスキーマの名前を確認します。 オブジェクトが既定の (**dbo**) スキーマ以外のスキーマに属している場合は、*schema_name.object_name* という 2 部構成の形式を使用してテーブルやオブジェクトの名前を指定する必要があります。  
  
-   オブジェクトがシステム テーブルに存在することを確認します。 テーブルやその他のスキーマ スコープ オブジェクトが存在するかどうかを確認するには、[sys.objects](/sql/relational-databases/system-catalog-views/sys-objects-transact-sql) カタログ ビューでクエリします。 オブジェクトがシステム テーブルにない場合、そのオブジェクトは削除されたか、ユーザーにオブジェクト メタデータを表示する権限がないかのいずれかです。 オブジェクト メタデータの表示方法の詳細については、「[メタデータ表示の構成](../security/metadata-visibility-configuration.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [カタログ ビュー &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)  
  
  
