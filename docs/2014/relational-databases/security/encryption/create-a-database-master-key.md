---
title: データベース マスター キーの作成 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2019
ms.prod: sql-server-2014
ms.reviewer: carlrab
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- database master key [SQL Server], creating
ms.assetid: 8cb24263-e97d-4e4d-9429-6cf494a4d5eb
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 86f74710e99079d0acd28db09bcf1e4ba7c57865
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957246"
---
# <a name="create-a-database-master-key"></a>データベース マスター キーの作成

このトピックでは、で`master` [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]を使用[!INCLUDE[tsql](../../../includes/tsql-md.md)]して、データベースにデータベースマスターキーを作成する方法について説明します。

**このトピックの内容**

- **作業を開始する準備:**

  [保護](#Security)

- [Transact-sql を使用してデータベースマスターキーを作成するには](#TsqlProcedure)

## <a name="BeforeYouBegin"></a>開始する前に

### <a name="Security"></a>保護

#### <a name="Permissions"></a>許可

データベースに対する CONTROL 権限が必要です。

## <a name="TsqlProcedure"></a>Transact-sql の使用

### <a name="to-create-a-database-master-key"></a>データベース マスター キーを作成するには

1. データベースに格納するマスター キーのコピーを暗号化するためのパスワードを指定します。
2. 
  **オブジェクト エクスプローラー**で、 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]のインスタンスに接続します。
3. 
  **[システム データベース]** を展開し、`master` を右クリックして、**[新しいクエリ]** をクリックします。
4. 次の例をコピーしてクエリ ウィンドウに貼り付け、 **[実行]** をクリックします。

  ```sql
  -- Creates the master key.
  -- The key is encrypted using the password "23987hxJ#KL95234nl0zBe."
  CREATE MASTER KEY ENCRYPTION BY PASSWORD = '23987hxJ#KL95234nl0zBe';
```

詳細については、[CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)を参照してください。
