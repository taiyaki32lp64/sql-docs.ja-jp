---
title: ポリシーベースの管理を使用したサーバーの管理
description: ポリシーベースの管理を使用して 1 つまたは複数の SQL Server インスタンスを管理する方法について説明します。
ms.custom: seo-lt-2019
ms.date: 08/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- facet See facets
- Declarative Management Framework See Policy-Based Management
- surface area configuration [SQL Server], Policy-Based Management
- Policy-Based Management
- facets [Policy-Based Management]
- Policy-Based Management, administering
- conditions [Policy-Based Management]
- facets [Policy-Based Management], about facets
- PolicyAdministratorRole role
ms.assetid: ef2a7b3b-614b-405d-a04a-2464a019df40
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 6e0abb97eddddc65103bfaad7c2e1996423a4919
ms.sourcegitcommit: 035ad9197cb9799852ed705432740ad52e0a256d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/31/2019
ms.locfileid: "75558682"
---
# <a name="administer-servers-by-using-policy-based-management"></a>ポリシー ベースの管理を使用したサーバーの管理
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
   ポリシー ベースの管理とは、1 つ以上の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスを管理するためのポリシー ベースのシステムのことです。 条件式を含む条件を作成します。 次に、作成した条件を対象のデータベース オブジェクトに適用するポリシーを作成します。  

たとえば、データベース管理者として、特定のサーバーでデータベース メールが有効になっていないことを確認することが必要があるとします。その場合は、そのサーバー オプションを設定した条件とポリシーを作成します。 
   
 > **重要!!** ポリシーは、一部の機能の動作に影響を及ぼすことがあります。 たとえば、変更データ キャプチャとトランザクション レプリケーションでは、インデックスがない systranschemas テーブルが使用されます。 すべてのテーブルにインデックスが必要であるというポリシーを有効にして、このポリシーへの準拠を適用した場合、これらの機能が失敗します。  
  
 SQL Server Management Studio を使用してポリシーを作成し管理するには
  
1.  構成するプロパティを含むポリシー ベースの管理ファセットを選択します。  
  
2.  管理ファセットの状態を指定する条件を定義します。  
  
3.  条件、対象セットをフィルター処理する追加条件、および評価モードを示すポリシーを定義します。  
  
4.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスがポリシーに準拠しているかどうかを確認します。  
  
 ポリシーに違反する場合は、オブジェクト エクスプローラーで、対象およびオブジェクト エクスプローラー ツリーの上位にあるノードの横に、重大な状態の警告が赤いアイコンとして示されます。  
  
> **注:** ポリシーのオブジェクト セットをシステムが計算する際、既定ではシステム オブジェクトが除外されます。  たとえば、ポリシーのオブジェクト セットがすべてのテーブルを参照する場合、システム テーブルにはそのポリシーが適用されません。 システム オブジェクトに対してポリシーを評価する必要がある場合は、ユーザーが、それらのオブジェクト セットに対し、システム オブジェクトを明示的に追加できます。 **"スケジュールに基づいて確認"** の評価モードではすべてのポリシーがサポートされますが、パフォーマンス上の理由により、 **"変更時に確認"** の評価モードでは、任意のオブジェクト セットを含んだポリシーは、必ずしもすべてサポートされるとは限りません。 詳細については、[https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx](https://blogs.msdn.com/b/sqlpbm/archive/2009/04/13/policy-evaluation-modes.aspx) を参照してください。  
  
## <a name="three-policy-based-management-components"></a>ポリシー ベースの管理は 3 つの要素で構成されます。  
 ポリシー ベースの管理は 3 つの要素で構成されます。  
  
-   ポリシー管理。 ポリシー管理者がポリシーを作成します。  
  
-   明示的な管理。 管理者が 1 つ以上の管理対象を選択し、対象が特定のポリシーに準拠しているかどうかを明示的に確認するか、対象をポリシーに明示的に準拠させます。  
  
-   評価モード。 実行モードには次の 4 種類があり、そのうち 3 つは自動化できます。  
  
    -   **[要求時]** : このモードでは、ユーザーが直接指定した場合にポリシーが評価されます。  
  
    -   **[変更時: 回避]** : この自動モードでは、DDL トリガーを使用してポリシー違反が防止されます。  
  
        > **重要:** nested triggers サーバー構成オプションが無効になっている場合、 **[変更時: 回避]** は正しく動作しません。 ポリシー ベースの管理では、この評価モードを使用するポリシーに準拠しない DDL 操作の検出およびロールバックに DDL トリガーが使用されます。 ポリシー ベースの管理の DDL トリガーを削除するか、nested triggers を無効にすると、この評価モードが失敗したり、予期しない動作をすることがあります。  
  
    -   **[変更時: ログのみ]** : この自動モードでは、関連する変更が行われたときにイベント通知を使用してポリシーが評価されます。  
  
    -   **[スケジュールで実行]** : この自動モードでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを使用してポリシーが定期的に評価されます。  
  
     自動ポリシーが有効になっていない場合、ポリシー ベースの管理はシステム パフォーマンスに影響しません。  
  
## <a name="terms"></a>Terms  
 **ポリシー ベースの管理の管理対象** ポリシー ベースの管理で管理するエンティティ ([!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] のインスタンス、データベース、テーブル、インデックスなど)。 サーバー インスタンス内のすべての対象で、対象となる階層が構成されます。 対象セットは、対象となる階層に一連の対象フィルターを適用した結果得られる一連の対象です (HumanResources スキーマが所有するデータベース内のすべてのテーブルなど)。  
  
 **ポリシー ベースの管理ファセット** 特定の種類の管理対象の動作または特性をモデル化した一連の論理プロパティ。 プロパティの数と特性がファセットに組み込まれ、その追加や削除はファセットの作成者のみが実行できます。 1 種類の対象で 1 つ以上の管理ファセットを実装したり、1 種類以上の対象で 1 つの管理ファセットを実装したりすることができます。 ファセットのプロパティの中には、特定のバージョンにしか適用できないものもあります。  
  
 **ポリシー ベースの管理条件**  
 管理ファセットについて、ポリシー ベースの管理の管理対象の一連の許可状態を指定するブール式。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、条件の評価時に照合順序に従おうとします。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の照合順序が Windows の照合順序と一致しないときは、条件をテストして、アルゴリズムによる競合の解決方法を調べてください。  
  
 **ポリシー ベースの管理ポリシー**  
 ポリシー ベースの管理条件と、評価モード、対象フィルター、スケジュールなどの想定される動作。 1 つのポリシーには 1 つの条件しか含めることができません。 ポリシーは有効または無効にできます。 ポリシーは msdb データベースに格納されます。  
  
 **ポリシー ベースの管理のポリシー カテゴリ**  
 ポリシーの管理に役立つユーザー定義のカテゴリ。 ユーザーは、ポリシーをさまざまなポリシー カテゴリに分類できます。 ポリシーは 1 つのポリシー カテゴリだけに属します。 ポリシー カテゴリはデータベースとサーバーに適用されます。 データベース レベルでは、次の条件が適用されます。  
  
-   データベース所有者は、データベースを一連のポリシー カテゴリにサブスクライブできます。  
  
-   そのサブスクライブ先のカテゴリのポリシーのみがデータベースを制御できます。  
  
-   データベースはすべて、既定のポリシー カテゴリに暗黙的にサブスクライブしています。  
  
 サーバー レベルでは、すべてのデータベースにポリシー カテゴリを適用できます。  
  
 **有効なポリシー**  
 対象の有効なポリシーとは、この対象を制御するポリシーのことです。 ポリシーは、次のすべての条件を満たす場合にのみ対象について有効になります。  
  
-   ポリシーが有効になっている。  
  
-   対象がポリシーの対象セットに属している。  
  
-   対象または対象のいずれかの先祖がこのポリシーを含んでいるポリシー グループにサブスクライブしている。  
  
## <a name="links-to-specific-tasks"></a>特定のタスクへのリンク 

 - [ポリシー ベースの管理のストレージ](policy-based-management-storage.md)|  
 - [ポリシー管理者にポリシー エラーを通知する警告の構成](../../relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)  
 - [新しいポリシーベースの管理条件の作成](../../relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md) 
 - [ポリシーベースの管理条件の削除](../../relational-databases/policy-based-management/delete-a-policy-based-management-condition.md)
 - [ポリシー ベースの管理条件のプロパティの表示または変更](../../relational-databases/policy-based-management/view-or-modify-the-properties-of-a-policy-based-management-condition.md)|  
 - [ポリシーベースの管理ポリシーのエクスポート](../../relational-databases/policy-based-management/export-a-policy-based-management-policy.md)
 - [ポリシー ベースの管理ポリシーのインポート](../../relational-databases/policy-based-management/import-a-policy-based-management-policy.md)|  
 - [オブジェクトからのポリシーベースの管理ポリシーの評価](../../relational-databases/policy-based-management/evaluate-a-policy-based-management-policy-from-an-object.md)
 - [ポリシー ベースの管理ファセットの操作](../../relational-databases/policy-based-management/working-with-policy-based-management-facets.md)|  
 - [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)


## <a name="see-also"></a>参照  
 
 - [チュートリアル:"既定でオフ" ポリシーの作成と適用](lesson-1-create-and-apply-an-off-by-default-policy.md)
 - [チュートリアル:名前付け基準ポリシーの作成と適用](lesson-2-create-and-apply-a-naming-standards-policy.md)
 - [ポリシーベースの管理ビュー &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)  
 

 
  
  
