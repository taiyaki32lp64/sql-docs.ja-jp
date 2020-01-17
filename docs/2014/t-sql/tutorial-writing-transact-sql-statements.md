---
title: チュートリアル:Transact-SQL ステートメントの作成 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: t-sql
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL statements, tutorials
- Transact-SQL tutorials
- tutorials [Transact-SQL]
ms.assetid: 2addc9be-67d0-423d-a457-192fe9d7d058
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 67e09713fdec72313bde6ba81e1cc169467fda0c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211198"
---
# <a name="tutorial-writing-transact-sql-statements"></a>チュートリアル:Transact-SQL ステートメントの作成
  [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントの作成チュートリアルへようこそ。 このチュートリアルは、SQL ステートメントを初めて作成するユーザーを対象としています。 ここでは初心者のユーザーを対象に、テーブルを作成し、データを挿入するための基本的なステートメントを紹介します。 このチュートリアルでは、 [!INCLUDE[tsql](../includes/tsql-md.md)]製品に実装されている SQL 規格の [!INCLUDE[msCoName](../includes/msconame-md.md)] を使用します。 このチュートリアルは、 [!INCLUDE[tsql](../includes/tsql-md.md)] 言語を簡単に紹介することを目的としています。 [!INCLUDE[tsql](../includes/tsql-md.md)] クラスの代わりとなるものではありません。 このチュートリアルで使用するステートメントは意図的に簡潔化されており、通常の実稼働データベースに見られる複雑性を表すものではありません。  
  
> [!NOTE]  
>  データベースの初心者ユーザーは、[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ステートメントを作成する代わりに、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] を使用して [!INCLUDE[tsql](../includes/tsql-md.md)] を操作した方が通常は簡単です。  
  
## <a name="finding-more-information"></a>詳細情報  
 特定のステートメントの詳細については、SQL Server オンライン ブックで名前を指定してステートメントを検索するか、[コンテンツ] を使用して、[Transact-SQL リファレンス (データベース エンジン)](/sql/t-sql/language-reference) の下にアルファベット順に列挙されている 1,800 の言語要素を参照してください。 情報を検索する別の方法として、興味のある内容に関連するキーワードを検索する方法があります。 たとえば、日付の一部 (月など) を返す方法を求めるには、**日付 [SQL Server]** のインデックスを検索し、**日付要素**を選択します。 これにより、トピック [「DATEPART (Transact-SQL)」](/sql/t-sql/functions/datepart-transact-sql) が表示されます。 別の例として、文字列の操作方法を求めるには、**文字列関数**を検索します。 これにより、トピック [「文字列関数 (Transact-SQL)」](/sql/t-sql/functions/string-functions-transact-sql) が表示されます。  
  
## <a name="what-you-will-learn"></a>学習する内容  
 このチュートリアルでは、データベースの作成、データベースのテーブルの作成、テーブルへのデータの挿入、データの更新、読み取り、削除、およびテーブルの削除の方法を示します。 ユーザーは、ビューやストアド プロシージャを作成し、データベースとデータのユーザーを構成します。  
  
 このチュートリアルは、次の 3 つのレッスンで構成されています。  
  
 [レッスン 1:データベース オブジェクトの作成](lesson-1-creating-database-objects.md)  
 このレッスンでは、データベースを作成し、データベースにテーブルを作成し、データをテーブルに挿入します。さらに、データを更新し、読み取ります。  
  
 [レッスン 2:データベース オブジェクトに対するアクセス許可の構成](lesson-2-configuring-permissions-on-database-objects.md)  
 このレッスンでは、ログインとユーザーを作成します。 また、ビューとストアド プロシージャも作成し、ストアド プロシージャにユーザー権限を与えます。  
  
 [レッスン 3:データベース オブジェクトの削除](lesson-3-1-deleting-database-objects.md)  
 このレッスンでは、データへのアクセス権を削除し、データをテーブルから削除し、テーブル、次にデータベースを削除します。  
  
## <a name="requirements"></a>必要条件  
 このチュートリアルを完了するにあたって SQL 言語に関する知識は必要ありませんが、テーブルなどの基本的なデータベース概念は理解している必要があります。 このチュートリアルでは、データベースと Windows ユーザーを作成します。 これらのタスクには高レベルのアクセス許可が必要なので、コンピューターには管理者としてログインしてください。  
  
 システムには次のコンポーネントがインストールされている必要があります。  
  
-   任意のエディションの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] または Management Studio Express  
  
-   Internet Explorer 6 以降。  
  
> [!NOTE]  
>  追加することをお勧め、チュートリアルを確認するとき、**次**と**前**ドキュメント ビューアーのツールバーのボタン。  
  
  
