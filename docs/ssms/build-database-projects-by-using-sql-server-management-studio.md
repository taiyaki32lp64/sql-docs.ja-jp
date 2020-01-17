---
title: SQL Server Management Studio によるデータベース プロジェクトのビルド | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server], database projects
- database projects [SQL Server]
- projects [SQL Server Management Studio], about projects
- projects [SQL Server Management Studio]
ms.assetid: c2e80045-894d-44cf-b65c-e547ed738947
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07dfe77992cb5e0e8011424d9cea878063a18943
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267609"
---
# <a name="build-database-projects-by-using-sql-server-management-studio"></a>SQL Server Management Studio によるデータベース プロジェクトのビルド
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
データベース スクリプト プロジェクトは、データベースやデータベースの一部に関連付けられているスクリプト、接続情報、およびテンプレートを組織的にまとめたものです。 [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] では、スクリプト プロジェクトのコンテキスト内の [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] データベースの管理やデザインに使用できる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] を提供しています。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] には、データベースの開発、配置、管理に役立つ、デザイナー、エディター、ガイド、およびウィザードが含まれています。  
  
## <a name="sql-server-management-studio"></a>SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] は、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のコンポーネントの管理に使用する管理ツールのセットです。 この統合環境を使用すると、データのバックアップやクエリの編集、共通関数の自動化など、さまざまな作業を 1 つのインターフェイスから実行できます。  
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] には以下のツールが含まれています。  
  
-   コード エディター。豊富な機能を持つスクリプト エディターで、スクリプトの作成や編集に使用します。 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] のコード エディターには、 [!INCLUDE[ssDE](../includes/ssde_md.md)] クエリ エディター ( [!INCLUDE[tsql](../includes/tsql-md.md)] スクリプト用)、DMX クエリ エディター、MDX クエリ エディター、および XML/A クエリ エディターの 4 種類のバージョンがあります。  
  
-   オブジェクト エクスプローラー。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに所属するオブジェクトの検索、変更、スクリプト作成、実行に使用します。  
  
-   テンプレート エクスプローラー。テンプレートの検索およびスクリプト作成に使用します。  
  
-   ソリューション エクスプローラー。プロジェクトに含まれる関連スクリプトの編成および格納に使用します。  
  
-   プロパティ ウィンドウ。選択したオブジェクトの現在のプロパティの表示に使用します。  
  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] は、以下の機能を提供して効率的な作業プロセスをサポートします。  
  
-   非接続アクセス。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]のインスタンスに接続しないで、スクリプトを作成および編集できます。  
  
-   すべてのダイアログ ボックスからのスクリプト作成。 どのダイアログ ボックスからでもスクリプトを作成できるので、スクリプト作成後に、これを読み取り、編集、格納、再利用できます。  
  
-   非モーダル ダイアログ ボックス。 UI ダイアログ ボックスにアクセスしたときに、そのダイアログ ボックスを閉じなくても、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の他のリソースを参照できます。  
  
## <a name="solutions-and-script-projects"></a>ソリューションおよびスクリプト プロジェクト  
ソリューション エクスプローラーは、データベース ソリューションを保存したり、再度開くためのユーティリティです。 ソリューションは、関連するスクリプト プロジェクトとファイルを編成したものです。 スクリプト プロジェクトには、 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] スクリプト ファイル、SQL テンプレート、接続情報、およびその他のファイルが格納されています。 スクリプトをスクリプト プロジェクト内に保存すると、次の操作が可能になります。  
  
-   スクリプトのバージョン管理。  
  
-   スクリプトを使用した結果オプションの保存。  
  
-   関連するスクリプトを 1 つのスクリプト プロジェクトに編成。  
  
-   スクリプトを使用した接続情報の保存。  
  
ソリューション エクスプローラーは、同じプロジェクトに関連するスクリプトの作成および再利用を支援するツールです。 同じような作業が後で必要になった場合、プロジェクトに保存されている一連のスクリプトを使用できます。 [!INCLUDE[msCoName](../includes/msconame_md.md)] [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を使用してアプリケーションを作成したことがあるユーザーにとって、ソリューション エクスプローラーはとてもなじみやすいものです。  
  
ソリューションは、1 つ以上のスクリプト プロジェクトで構成されています。 プロジェクトは、1 つ以上のスクリプトまたは接続で構成されています。 プロジェクトには、スクリプト以外のファイルも含まれる場合があります。  
  
## <a name="see-also"></a>参照  
[SQL Server Management Studio の使用 [SQL Server]](../ssms/use-sql-server-management-studio.md)  
[SQL Server Management Studio によるクエリの作成、分析、編集](https://msdn.microsoft.com/062051e4-4b77-4969-98ae-d2547c24ce3e)  
[ソリューション (SQL Server Management Studio)](../ssms/solution/solutions-sql-server-management-studio.md)  
  
