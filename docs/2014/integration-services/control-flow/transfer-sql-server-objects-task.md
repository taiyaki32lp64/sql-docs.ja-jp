---
title: SQL Server オブジェクトの転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfersqlserverobjectstask.f1
helpviewer_keywords:
- Transfer SQL Server Objects task [Integration Services]
ms.assetid: fe86d6e5-e415-406c-88f3-dc3ef71bd5f0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 01b985a1bb818e7b3d3612596bb4e2b7fa6fd393
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62829461"
---
# <a name="transfer-sql-server-objects-task"></a>SQL Server オブジェクトの転送タスク
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベース内の 1 つ以上の種類のオブジェクトを [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間で転送します。 たとえば、このタスクを使用して、テーブルやストアド プロシージャをコピーできます。 転送元として使用される [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のバージョンに応じて、コピーできるオブジェクトの種類が異なります。 たとえば、スキーマとユーザー定義集計は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースだけに含まれます。  
  
## <a name="objects-to-transfer"></a>転送するオブジェクト  
 転送するオブジェクトの権限に加えて、指定したデータベースのサーバー ロール、ロール、およびユーザーもコピーできます。 関連付けられているユーザー、ロール、および権限をオブジェクトと一緒にコピーすることで、転送したオブジェクトを転送先サーバー上ですぐに利用できます。  
  
 次の表に、コピーできるオブジェクトを示します。  
  
|オブジェクト|  
|------------|  
|テーブル|  
|ビュー|  
|ストアド プロシージャ|  
|ユーザー定義関数|  
|デフォルト|  
|ユーザー定義のデータ型|  
|パーティション関数|  
|パーティション構成|  
|スキーマ|  
|アセンブリ|  
|ユーザー定義集計|  
|ユーザー定義型|  
|XML スキーマ コレクション|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスで作成されたユーザー定義型 (UDT) には、共通言語ランタイム (CLR) アセンブリに対する依存関係があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを使用して UDT を転送する場合、依存オブジェクトを転送するタスクを構成する必要もあります。 依存オブジェクトを転送するには、`IncludeDependentObjects` プロパティを `True` に設定します。  
  
### <a name="table-options"></a>テーブル オプション  
 テーブルをコピーする際には、コピー プロセスに含めるテーブル関連のアイテムの種類を指定できます。 次の種類のアイテムは、関連するテーブルと共にコピーできます。  
  
-   インデックス  
  
-   トリガー  
  
-   フルテキスト インデックス  
  
-   主キー  
  
-   外部キー  
  
 また、タスクで生成するスクリプトを Unicode 形式にするかどうかも指定できます。  
  
## <a name="destination-options"></a>転送先に関するオプション  
 転送するオブジェクトのスキーマ名、データ、拡張プロパティ、および依存オブジェクトを転送に含めるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成できます。 データをコピーする場合、置換するか、既存のデータを追加できます。  
  
 一部のオプションは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のみに適用されます。 たとえば、スキーマは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] でのみサポートされます。  
  
## <a name="security-options"></a>セキュリティ オプション  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、転送元の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースレベルのユーザーとロール、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン、および転送するオブジェクトの権限を含めることができます。 たとえば、転送するテーブルの権限を転送に含めることができます。  
  
## <a name="transfer-objects-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのオブジェクトの転送  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の転送元および転送先をサポートします。  
  
## <a name="events"></a>イベント  
 このタスクは、転送されたオブジェクトを報告する情報イベントを生成する以外に、オブジェクトが上書きされたときに警告イベントを生成します。 情報イベントは、データベース テーブルの切り捨てなどのアクションに対しても生成されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクでは、オブジェクト転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 このタスクの `ExecutionValue` プロパティに格納される実行値は、転送されたオブジェクトの数を返します。 SQL Server オブジェクトの転送タスクの `ExecValueVariable` プロパティにユーザー定義変数を割り当てると、オブジェクト転送に関する情報をパッケージの他のオブジェクトで使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](../use-variables-in-packages.md)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 SQL Server オブジェクトの転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferSqlServerObjectsTaskStartTransferringObjects   転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferSqlServerObjectsTaskFinishedTransferringObjects    転送が完了したことを報告このログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、`OnInformation` イベントのログ エントリは、転送対象として選択された種類のオブジェクトの数、転送されたオブジェクトの数、およびテーブルと一緒にデータが転送されたときはテーブルの切り捨てなどのアクションを報告します。 `OnWarning` イベントのログ エントリは転送先でオブジェクトが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 ユーザーは、転送元サーバー上でオブジェクトを参照する権限、および転送先サーバー上でオブジェクトを削除および作成する権限を持っていることに加えて、指定したデータベースおよびデータベース オブジェクトにアクセスできる必要があります。  
  
## <a name="configuration-of-the-transfer-sql-server-objects-task"></a>SQL Server オブジェクトの転送タスクの構成  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成して、すべてのオブジェクト、特定の種類のすべてのオブジェクト、または特定の種類の指定したオブジェクトを転送の対象とすることができます。 たとえば、AdventureWorks データベース内の選択したテーブルのみをコピーするように指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを使用してテーブルを転送する場合は、テーブルと一緒にコピーする、テーブルに関連するオブジェクトの種類を指定できます。 たとえば、テーブルと一緒に主キーをコピーするように指定できます。  
  
 転送するオブジェクトの機能をさらに強化するため、転送するオブジェクトのスキーマ名、データ、拡張プロパティ、および依存オブジェクトを転送に含めるように [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクを構成できます。 データをコピーする場合は、既存のデータを置き換えるかまたは追加するかを指定できます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは実行時、2 つの SMO 接続マネージャーを使用して、転送元サーバーおよび転送先サーバーに接続します。 SMO 接続マネージャーの構成は [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクとは別に行い、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] オブジェクトの転送タスクは SMO 接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、サーバーに接続する際に使用する認証モードを指定します。 詳しくは、「 [SMO 接続マネージャー](../connection-manager/smo-connection-manager.md)」をご覧ください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックのいずれかを参照してください。  
  
-   [[SQL Server オブジェクトの転送タスク エディター] &#40;[全般] ページ&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [[SQL Server オブジェクトの転送タスク エディター] &#40;[オブジェクト] ページ&#41;](../transfer-sql-server-objects-task-editor-objects-page.md)  
  
-   [[式] ページ](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-sql-server-objects-task"></a>プログラムによる SQL Server オブジェクトの転送タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferSqlServerObjectsTask.TransferSqlServerObjectsTask>  
  
  
