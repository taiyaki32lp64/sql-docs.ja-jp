---
title: "レプリケーションのスクリプト作成 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9889d43aeed7cf80f5b28b427787519ab06bd84
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="scripting-replication"></a>レプリケーションのスクリプト作成
  トポロジ内のすべてのレプリケーション コンポーンネントは、災害復旧計画の一部としてスクリプト化され、スクリプトはタスクの繰り返しの自動化にも使用することができます。 スクリプトには、パブリケーションやサブスクリプションなどスクリプト化されたレプリケーション コンポーネントを実装するために必要な Transact-SQL システム ストアド プロシージャが格納されます。 スクリプトはウィザード (パブリケーションの新規作成ウィザードなど) で作成することができ、コンポーネントの作成後、 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用して作成することもできます。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] または **sqlcmd**を使用すると、スクリプトの表示、変更、および実行を行うことができます。 スクリプトをバックアップ ファイルと共に保存して、レプリケーション トポロジの再構成が必要な場合に使用できます。  
  
 プロパティが変更された場合は、コンポーネントのスクリプトを再作成する必要があります。 トランザクション レプリケーションでカスタム ストアド プロシージャを使用している場合は、各プロシージャのコピーをスクリプトと共に保存しておく必要があります。プロシージャが変更された場合は、プロシージャのコピーも更新する必要があります (スキーマやアプリケーション要件が変更されると、通常、プロシージャが更新されます)。 カスタム プロシージャの詳細については、「[トランザクション アーティクルに変更を反映する方法の指定](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)」を参照してください。  
  
 パラメーター化されたフィルターを使用するマージ パブリケーションの場合、パブリケーション スクリプトには、データ パーティションを作成するためのストアド プロシージャの呼び出しが含まれます。 このスクリプトによって、作成されたパーティションの参照、および必要に応じて 1 つ以上のパーティションを再作成する方法を利用できます。  
  
## <a name="example-of-automating-a-task-with-scripts"></a>スクリプトによるタスクの自動化の例  
 たとえば、 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]では、リモートの営業部門にデータを配信するマージ レプリケーションを実装しているとします。 営業担当者は、プル サブスクリプションを使用して自分の販売区域内の顧客に関連するすべてのデータをダウンロードします。 オフラインで作業しているときには、データを更新したり、新しい顧客や受注を入力することができます。 [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] には、さまざまな区域に 50 人を超える営業担当者がいるため、サブスクリプションの新規作成ウィザードを使用してサブスクライバーごとにさまざまなサブスクリプションを作成するには時間がかかります。 代わりに、レプリケーション管理者は次の手順を実行します。  
  
1.  営業担当者または販売区域に基づいたパーティションで必要なマージ パブリケーションを設定します。  
  
2.  1 つのサブスクライバーに対して 1 つのプル サブスクリプションを作成します。  
  
3.  作成したプル サブスクリプションに基づいてスクリプトを生成します。  
  
4.  スクリプトを変更し、サブスクライバーの名前などの値を変更します。  
  
5.  複数のサブスクライバーでスクリプトを実行し、必要なプル サブスクリプションを生成します。  
  
## <a name="script-replication-objects"></a>レプリケーション オブジェクトのスクリプトの作成  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のレプリケーション ウィザード、または **[レプリケーション]** フォルダーからレプリケーション オブジェクトのスクリプトを作成します。 ウィザードからスクリプトを作成する場合は、オブジェクトの作成後にスクリプトを作成するか、スクリプトの作成のみを行うかを選択することができます。  
  
> [!IMPORTANT]  
>  すべてのパスワードは NULL としてスクリプトが作成されます。 可能であれば、実行時、ユーザーに対してセキュリティ資格情報の入力を要求します。 スクリプト ファイルに資格情報を格納する場合は、不正アクセスを防ぐために、そのファイルをセキュリティで保護する必要があります。  
  
 レプリケーション ウィザードの使用方法の詳細については、以下を参照してください。  
  
-   [パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)  
  
-   [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [Create a Push Subscription](../../relational-databases/replication/create-a-push-subscription.md)  
  
-   [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>レプリケーション ウィザードからオブジェクトのスクリプトを作成するには  
  
1.  ウィザードの **[ウィザードのアクション]** ページで、ウィザードに対して適切なチェック ボックスをオンにします。  
  
    -   **[パブリケーションを作成するためのステップを含むスクリプト ファイルを生成する]**  
  
    -   **[サブスクリプションを作成するためのステップを含むスクリプト ファイルを生成する]**  
  
    -   **[ディストリビューションを構成するためのステップを含むスクリプトを生成する]**  
  
2.  **[スクリプト ファイルのプロパティ]** ページでオプションを指定します。  
  
3.  ウィザードを完了します。  
  
#### <a name="to-script-an-object-from-management-studio"></a>Management Studio からオブジェクトのスクリプトを作成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でディストリビューター、パブリッシャー、またはサブスクライバーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを展開し、 **[ローカル パブリケーション]** フォルダーまたは **[ローカル サブスクリプション]** フォルダーを展開します。  
  
3.  パブリケーションまたはサブスクリプションを右クリックし、 **[スクリプトの生成]**をクリックします。  
  
4.  **[SQL スクリプトの生成 - \<ReplicationObject>]** ダイアログ ボックスでオプションを指定します。  
  
5.  **[スクリプトをファイルに保存]**をクリックします。  
  
6.  **[スクリプト ファイルの場所]** ダイアログ ボックスでファイル名を入力し、 **[保存]**をクリックします。 状態メッセージが表示されます。  
  
7.  **[OK]**をクリックし、 **[閉じる]**をクリックします。  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>Management Studio から複数のオブジェクトのスクリプトを作成するには  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]でディストリビューター、パブリッシャー、またはサブスクライバーに接続し、サーバー ノードを展開します。  
  
2.  **[レプリケーション]** フォルダーを右クリックし、 **[スクリプトの生成]**をクリックします。  
  
3.  **[SQL スクリプトの生成]** ダイアログ ボックスでオプションを指定します。  
  
4.  **[スクリプトをファイルに保存]**をクリックします。  
  
5.  **[スクリプト ファイルの場所]** ダイアログ ボックスでファイル名を入力し、 **[保存]**をクリックします。 状態メッセージが表示されます。  
  
6.  **[OK]** をクリックし、 **[閉じる]**をクリックします。  
  
  