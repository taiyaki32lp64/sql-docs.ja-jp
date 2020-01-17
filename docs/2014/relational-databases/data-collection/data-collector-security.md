---
title: データ コレクターのセキュリティ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collection [SQL Server]
- security [data collector]
- data collector [SQL Server], security
ms.assetid: e75d6975-641e-440a-a642-cb39a583359a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7dd2b26662fea95837eabaf61f61e3da04fac69
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62873617"
---
# <a name="data-collector-security"></a>データ コレクターのセキュリティ
  データ コレクターは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェントによって実装されるロールベースのセキュリティ モデルを使用します。 このモデルを使用すると、データベース管理者は、データ コレクターのさまざまなタスクをそのタスクの実行に必要な権限だけがあるセキュリティ コンテキスト内で実行できます。 この方法は、ストアド プロシージャかビューを使用しないとアクセスできない内部テーブルに関係する操作に対しても使用されます。 内部テーブルに対する権限は与えられず、 テーブルへのアクセスに使用されるストアド プロシージャやビューのユーザーに対して権限がチェックされます。  
  
> [!IMPORTANT]  
>  このセキュリティ モデルのもう 1 つの重要な側面は、同心構造権限です。 同心構造権限では、オブジェクト (警告、オペレーター、ジョブ、スケジュール、プロキシなど) に対して、高いレベルの特権を持つロールは、低いレベルの特権を持つロールの権限を継承します。 詳しくは、「 [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md)」をご覧ください。  
  
 ここでは、データ コレクションの全般的なセキュリティと、ユーザーがデータ コレクターを構成および使用したり、管理データ ウェアハウスに関連するタスクを実行したりするために必要なロールについて説明します。  
  
## <a name="general-security"></a>全般的なセキュリティ  
 データ コレクターは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]の文書化されている標準に従ってインストールされます。  
  
### <a name="network-security"></a>ネットワーク セキュリティ  
 対象のインスタンス、構成サーバーに関連付けられているリレーショナル インスタンス、実行中のコレクション セット、および管理データ ウェアハウスをホストするサーバーの間で、秘密情報がやり取りされる可能性があります。  
  
 ネットワークで送信されるデータを保護するために、標準のセキュリティ メカニズム ( [!INCLUDE[tsql](../../includes/tsql-md.md)]のプロトコル暗号化など) が実装されています。  
  
## <a name="permissions-for-configuring-and-using-the-data-collector"></a>データ コレクターの構成および使用のための権限  
 タスクによっては、ユーザーが、データ コレクターのために用意されている 1 つ以上の固定データベース ロールのメンバーである必要があります。 特権レベルの高いロールから順に、次に示します。  
  
-   `dc_admin`  
  
-   **dc_operator**  
  
-   **dc_proxy**  
  
 上記のロールは、msdb データベースに格納されています。 既定では、これらのデータベース ロールのメンバーであるユーザーはいません。 これらのロールのユーザー メンバーシップは、明示的に許可する必要があります。  
  
 メンバーであるユーザーの`sysadmin`固定サーバー ロールへのフル アクセスがある[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]エージェント オブジェクトとデータ コレクターのビュー。 しかし、これらのユーザーも、データ コレクターのロールに明示的に追加する必要があります。  
  
> [!IMPORTANT]  
>  db_ssisadmin ロールおよび dc_admin ロールのメンバーは、特権を sysadmin に昇格できる可能性があります。 このような特権の昇格が発生するのは、それらのロールが [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージを変更でき、 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] エージェントの sysadmin セキュリティ コンテキストを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] パッケージを実行できるためです。 メンテナンス プラン、データ コレクション セット、およびその他の [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] パッケージの実行時にこの特権の昇格を防ぐには、特権が制限されたプロキシ アカウントを使用するようにパッケージを実行する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント ジョブを構成するか、db_ssisadmin ロールおよび dc_admin ロールには sysadmin メンバーのみを追加するようにします。  
  
### <a name="dcadmin-role"></a>dc_admin ロール  
 ユーザーに割り当てられている、`dc_admin`ロールがデータ コレクターの構成への完全な管理者アクセス (作成、読み取り、更新、および Delete) をサーバー インスタンス上にあります。 このロールのメンバーが実行できる操作を以下に示します。  
  
-   コレクター レベルのプロパティの設定  
  
-   新しいコレクション セットの追加  
  
-   新しいコレクション型のインストール  
  
-   **dc_operator** ロールに対して許可されているすべての操作の実行  
  
 `dc_admin`ロールは、次の役割のメンバーです。  
  
-   **SQLAgentUserRole**。 スケジュールを作成したりジョブを実行したりするために必要です。  
  
    > [!NOTE]  
    >  データ コレクターへのアクセスを許可する必要があります用に作成されたプロキシ`dc_admin`それらを作成し、プロキシを必要とするジョブ ステップで使用します。  
  
-   **dc_operator**。 メンバーの`dc_admin`に付与されたアクセス許可を継承**dc_operator**します。  
  
### <a name="dcoperator-role"></a>dc_operator ロール  
 **dc_operator** ロールのメンバーには、読み取りと更新のアクセス権が与えられます。 このロールは、コレクション セットの実行と構成に関連する操作タスクをサポートします。 このロールのメンバーが実行できる操作を以下に示します。  
  
-   コレクション セットの開始または停止  
  
-   既存のコレクション セットの列挙  
  
-   コレクション セットに関連付けられている詳細情報 (コレクション アイテムや収集頻度など) の表示  
  
-   既存のコレクション セットのアップロード頻度の変更  
  
-   既存のコレクション セットに含まれるコレクション アイテムの収集頻度の変更  
  
 **dc_operator** ロールは、データ コレクター パッケージを列挙して表示するために必要な次のロールのメンバーです。  
  
-   **db_ssisltduser**  
  
-   **db_ssisoperator**  
  
 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。  
  
### <a name="dcproxy-role"></a>dc_proxy ロール  
 **dc_proxy** ロールのメンバーには、データ コレクターのコレクション セットとコレクター レベルのプロパティへの読み取りアクセス権が与えられます。 自身が所有するジョブを実行したり、既存のプロキシ アカウントとして実行するジョブ ステップを作成したりすることもできます。  
  
 このロールのメンバーが実行できる操作を以下に示します。  
  
-   コレクション セットの構成情報 (コレクション アイテムの入力パラメーターや収集頻度など) の表示  
  
-   署名されたストアド プロシージャしかアクセスできない暗号化された内部情報 (データのアップロードに使用されるデータ ウェアハウスの接続情報など) の取得  
  
-   コレクション セットの実行時イベントのログ記録  
  
 **dc_proxy** ロールは、データ コレクター パッケージを列挙して表示するために必要な次のロールのメンバーです。  
  
-   **db_ssisltduser**。  
  
-   **db_ssisoperator**  
  
 詳細については、「[Integration Services のロール &#40;SSIS サービス&#41;](../../integration-services/security/integration-services-roles-ssis-service.md)」を参照してください。  
  
## <a name="permissions-for-configuring-and-using-the-management-data-warehouse"></a>管理データ ウェアハウスの構成および使用のための権限  
 タスクによっては、ユーザーが、管理データ ウェアハウスへのアクセスのために用意されている 1 つ以上の固定データベース ロールのメンバーである必要があります。 特権レベルの高いロールから順に、次に示します。  
  
-   **mdw_admin**  
  
-   **mdw_writer**  
  
-   **mdw_reader**  
  
 上記のロールは、msdb データベースに格納されています。 既定では、これらのデータベース ロールのメンバーであるユーザーはいません。 これらのロールのユーザー メンバーシップは、明示的に許可する必要があります。  
  
 メンバーであるユーザーの`sysadmin`固定サーバー ロールがデータ コレクター ビューへのフル アクセスがあります。 しかし、その他の操作を実行するには、明示的にデータベース ロールに追加する必要があります。  
  
### <a name="mdwadmin-role"></a>mdw_admin ロール  
 **mdw_admin** ロールのメンバーには、管理データ ウェアハウスへの読み取り、書き込み、更新、および削除のアクセス権が与えられます。  
  
 このロールのメンバーが実行できる操作を以下に示します。  
  
-   管理データ ウェアハウスのスキーマを必要に応じて変更する (新しいコレクション型がインストールされたときに新しいテーブルを追加するなど)  
  
    > [!NOTE]  
    >  スキーマ変更では、ユーザーのメンバーであることも、`dc_admin`このアクションには、msdb のデータ コレクターの構成を更新するアクセス許可が必要なため、新しいコレクター型をインストールするロール。  
  
-   管理データ ウェアハウスのメンテナンス ジョブ (アーカイブやクリーンアップなど) を実行する  
  
### <a name="mdwwriter-role"></a>mdw_writer ロール  
 **mdw_writer** ロールのメンバーは、管理データ ウェアハウスへのデータのアップロードや書き込みを行うことができます。 管理データ ウェアハウスにデータを格納するデータ コレクターはすべてこのロールのメンバーである必要があります。  
  
### <a name="mdwreader-role"></a>mdw_reader ロール  
 **mdw_reader** ロールのメンバーには、管理データ ウェアハウスへの読み取りアクセス権が与えられます。 このロールの目的は、履歴データへのアクセスを提供してトラブルシューティングをサポートすることであるため、このロールのメンバーは、管理データ ウェアハウスのスキーマのその他の要素を表示することはできません。  
  
## <a name="see-also"></a>関連項目  
 [SQL Server エージェントのセキュリティの実装](../../ssms/agent/implement-sql-server-agent-security.md)  
  
  
