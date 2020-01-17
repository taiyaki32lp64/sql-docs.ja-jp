---
title: アセンブリの実装 |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- assemblies [CLR integration], implementing
ms.assetid: c228d7bf-a906-4f37-a057-5d464d962ff8
author: rothja
ms.author: jroth
ms.openlocfilehash: c6ca486f3464334c96c3b3874c4dfff71161e978
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018850"
---
# <a name="assemblies---implementing"></a>アセンブリ - 実装
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このトピックでは、データベースにアセンブリを実装し、それらのアセンブリを使用して作業するのに役立つ次の情報について説明します。  
  
-   アセンブリの作成  
  
-   アセンブリの変更  
  
-   削除、無効化、およびアセンブリを有効にします。  
  
-   アセンブリのバージョンを管理  
  
## <a name="creating-assemblies"></a>アセンブリの作成  
 アセンブリの作成は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY ステートメントを使用し、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ではアセンブリ支援エディターを使用して行います。 さらでの SQL Server プロジェクトを配置[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]プロジェクトの指定されたデータベースでアセンブリが登録されます。 詳細については、「 [CLR データベース オブジェクトの配置](../../relational-databases/clr-integration/deploying-clr-database-objects.md)」を参照してください。  
  
 **TRANSACT-SQL を使用してアセンブリを作成するには**  
  
-   [CREATE ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/create-assembly-transact-sql.md)  
  
 **SQL Server Management Studio を使用してアセンブリを作成するには**  
  
-   [アセンブリのプロパティ&#40;[全般] ページ&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="modifying-assemblies"></a>アセンブリの変更  
 アセンブリの変更は、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY ステートメントを使用し、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ではアセンブリ支援エディターを使用して行います。 次の操作を行うと、アセンブリを変更できます。  
  
-   アセンブリの新しいバージョンのバイナリをアップロードして、アセンブリの実装を変更します。 詳細については、次を参照してください。[アセンブリのバージョン管理](#_managing)このトピックで後述します。  
  
-   アセンブリの権限セットを変更します。 詳細については、「[アセンブリのデザイン](../../relational-databases/clr-integration/assemblies-designing.md)」を参照してください。  
  
-   アセンブリの表示設定を変更します。 表示されるアセンブリは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で参照できます。 表示されないアセンブリは、データベースにアップロードされている場合でも参照できません。 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアップロードされたアセンブリは表示されます。  
  
-   アセンブリに関連付けられているデバッグ ファイルやソース ファイルを追加または削除します。  
  
 **TRANSACT-SQL を使用してアセンブリを変更するには**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
 **SQL Server Management Studio を使用してアセンブリを変更するには**  
  
-   [アセンブリのプロパティ&#40;[全般] ページ&#41;](../../relational-databases/clr-integration/assemblies-properties.md)  
  
## <a name="dropping-disabling-and-enabling-assemblies"></a>アセンブリの削除、無効化、および有効化  
 アセンブリの削除は、[!INCLUDE[tsql](../../includes/tsql-md.md)] DROP ASSEMBLY ステートメントまたは [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して行います。  
  
 **TRANSACT-SQL を使用してアセンブリを削除するには**  
  
-   [DROP ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-assembly-transact-sql.md)  
  
 **SQL Server Management Studio を使用してアセンブリを削除するには**  
  
-   [オブジェクトの削除](../../ssms/object/delete-objects.md)  
  
 既定では、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で作成されたアセンブリがすべて実行できない状態になっています。 使用することができます、 **clr を有効になっている**のオプション、 **sp_configure**システム ストアド プロシージャにアップロードされているすべてのアセンブリの実行を有効または無効に[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]します。 アセンブリの実行を無効にすると、CLR (共通言語ランタイム) 関数、ストアド プロシージャ、トリガー、集計、およびユーザー定義型を実行できなくなり、現在実行されている場合は停止されます。 アセンブリの実行を無効にしても、アセンブリを作成、変更、または削除する機能は無効になりません。 詳細については、次を参照してください。 [clr enabled サーバー構成オプション](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)します。  
  
 **無効にし、アセンブリの実行を有効にします。**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
##  <a name="_managing"></a> アセンブリのバージョンを管理  
 アセンブリを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスにアップロードすると、そのアセンブリはデータベース システム カタログ内に格納され、管理されます。 内のアセンブリの定義に加えられた変更、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]データベース カタログに格納されているアセンブリを反映する必要があります。  
  
 アセンブリを変更する必要がある場合は、ALTER ASSEMBLY ステートメントを実行してデータベース内のアセンブリを更新する必要があります。 これにより、アセンブリの実装を保持している [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] モジュールの最新のコピーにアセンブリが更新されます。  
  
 ALTER ASSEMBLY ステートメントの WITH UNCHECKED DATA 句は、データベース内の永続化されたデータが依存しているアセンブリも最新状態に更新するように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に指示します。 具体的には、次のいずれかが存在する場合、WITH UNCHECKED DATA を指定する必要があります。  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] の関数またはメソッドによってアセンブリ内のメソッドを直接または間接的に参照する、永続化された計算列。  
  
-   アセンブリに依存する CLR ユーザー定義型の列と、**UserDefined** (非**ネイティブ**) シリアル化形式を実装する型の列。  
  
> [!CAUTION]  
>  WITH UNCHECKED DATA を指定せず、新しいバージョンのアセンブリによってテーブルの既存のデータ、インデックス、または他の固有サイトに影響が生じる場合、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では ALTER ASSEMBLY の実行回避が試みられます。 ただし、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] では、CLR アセンブリの更新時に、計算列、インデックス、インデックス付きビュー、または式が、基になるルーチンや型と一致することは保証されません。 ALTER ASSEMBLY を実行する場合は、式の結果とアセンブリ内の式に基づく値との間に不一致が生じないように注意する必要があります。  
  
 メンバーのみ、 **db_owner**と**db_ddlowner**固定データベース ロールは、WITH UNCHECKED DATA 句を使用して、ALTER ASSEMBLY を実行することができます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、テーブル内に未チェック データがある状態でアセンブリが変更されたというメッセージを Windows アプリケーション イベント ログに記録します。 さらに [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] は、そのアセンブリに依存するデータを含んでいるすべてのテーブルに、未チェック データを含むテーブルであるというマークを付けます。 **Has_unchecked_assembly_data**の列、 **sys.tables**カタログ ビューには、未チェック データ、未チェック データを含まないテーブルに対して 0 を含むテーブルでは、値 1 が含まれています。  
  
 未チェック データの整合性を解決するを持つ各テーブルに対して DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS を実行します。 未チェック データ。 DBCC CHECKDB WITH EXTENDED_LOGICAL_CHECKS が失敗した場合、いずれかが無効か、問題を解決するアセンブリ コードを変更するテーブルの行を削除して、その他の ALTER ASSEMBLY ステートメントを発行します。  
  
 ALTER ASSEMBLY ではアセンブリのバージョンが変更されます。 カルチャと、アセンブリの公開キー トークンは同じです。SQL Server では、同じ名前、カルチャ、および公開キーを別のバージョンのアセンブリを登録することはできません。  
  
### <a name="interactions-with-computer-wide-policy-for-version-binding"></a>バージョン バインディングでのコンピューター全体のポリシーとの相互作用  
 パブリッシャー ポリシーまたはコンピューター全体の管理者ポリシーを使用して、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] に格納されているアセンブリへの参照を特定のバージョンにリダイレクトする場合、次のいずれかを実行する必要があります。  
  
-   リダイレクト先の新しいバージョンがデータベースに格納されていることを確認します。  
  
-   すべてのステートメントをコンピューターの外部ポリシー ファイルまたはパブリッシャー ポリシーに変更して、データベースに格納されている特定のバージョンがステートメントによって参照されるようにします。  
  
 上記のいずれかの操作を実行しないと、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスに新しいアセンブリのバージョンをロードできません。  
  
 **アセンブリのバージョンを更新するには**  
  
-   [ALTER ASSEMBLY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-assembly-transact-sql.md)  
  
## <a name="see-also"></a>参照  
 [アセンブリ&#40;データベース エンジン&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [アセンブリに関する情報の取得](../../relational-databases/clr-integration/assemblies-getting-information.md)  
  
  
