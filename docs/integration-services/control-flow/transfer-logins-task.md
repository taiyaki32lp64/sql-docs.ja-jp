---
title: ログイン転送タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.transferloginstask.f1
- sql13.dts.designer.transferloginstask.general.f1
- sql13.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d82f3ef27525ad918ef01e9cb2e0600ef85ae0a
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71293860"
---
# <a name="transfer-logins-task"></a>ログイン転送タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  ログイン転送タスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のインスタンス間で 1 つ以上のログインを転送します。  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>SQL Server のインスタンス間でのログインの転送  
 ログイン転送タスクでは、転送元または転送先として、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] をサポートします。  
  
## <a name="events"></a>イベント  
 ログイン転送タスクでは、転送されたログインの数を報告する情報イベントと、ログインが上書きされた場合の警告イベントが発生します。  
  
 ログインの転送の進捗状況は報告されません。0% または 100% 完了した場合のみ報告されます。  
  
## <a name="execution-value"></a>実行値  
 タスクの **ExecutionValue** プロパティで定義する実行値は、転送されたログインの数を返します。 ログイン転送タスクの **ExecValueVariable** プロパティにユーザー定義変数を割り当てると、パッケージの他のオブジェクトからログインの転送に関する情報を使用できるようになります。 詳細については、「[Integration Services &#40;SSIS&#41; の変数](../../integration-services/integration-services-ssis-variables.md)」と「[パッケージで変数を使用する](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)」をご覧ください。  
  
## <a name="log-entries"></a>ログ エントリ  
 ログイン転送タスクには、次のようなカスタム ログ エントリがあります。  
  
-   TransferLoginsTaskStarTransferringObjects   転送が開始されたことを報告するログ エントリです。 ログ エントリには、開始時刻が含まれます。  
  
-   TransferLoginsTaskFinishedTransferringObjects   転送が完了したことを報告するログ エントリです。 ログ エントリには、終了時刻が含まれます。  
  
 また、 **OnInformation** イベントのログ エントリは転送されたログインの数を報告し、 **OnWarning** イベントのログ エントリは転送先でログインが上書きされると書き込まれます。  
  
## <a name="security-and-permissions"></a>セキュリティおよび権限  
 転送元サーバーのログインを参照し、転送先サーバーにログインを作成するユーザーは、両方のサーバーのサーバー ロール sysadmin のメンバーでなければなりません。  
  
## <a name="configuration-of-the-transfer-logins-task"></a>ログイン転送タスクの構成  
 ログイン転送タスクは、すべてのログイン、指定したログインのみ、または指定したデータベースにアクセスしたすべてのログインを転送するように構成できます。 sa ログインは転送できません。 sa ログインの名前は変更できますが、名前を変更した sa ログインを転送することはできません。  
  
 また、ログインに関連付けられているセキュリティ識別子 (SID) をコピーするかどうかも指定できます。 ログイン転送タスクをデータベース転送タスクと共に使用する場合、SID を転送先にコピーする必要があります。コピーしない場合、転送したログインが転送先データベースで認識されません。  
  
 転送先では、転送されたログインは無効にされ、ランダムなパスワードが割り当てられます。 ログインを使用する前に、転送先サーバーの sysadmin ロールのメンバーがパスワードを変更して、ログインを有効にする必要があります。  
  
 転送するログインが既に転送先に存在している場合もあります。 ログイン転送タスクでは、既存のログインの処理を次のように構成できます。  
  
-   既存のログインを上書きします。  
  
-   重複するログインが存在する場合、タスクを失敗とします。  
  
-   重複するログインをスキップします。  
  
 ログイン転送タスクは実行時に、2 つの SMO 接続マネージャーを使用して、転送元および転送先サーバーに接続します。 SMO 接続マネージャーの構成はログイン転送タスクとは別に行い、ログイン転送タスクは SMO 接続マネージャーを参照します。 SMO 接続マネージャーは、サーバーと、サーバーに接続する際に使用する認証モードを指定します。 詳しくは、「 [SMO 接続マネージャー](../../integration-services/connection-manager/smo-connection-manager.md)」をご覧ください。  
  
 プロパティを設定するには [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーから行うか、またはプログラムによって設定します。  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーで設定できるプロパティの詳細については、次のトピックを参照してください。  
  
-   [[式] ページ](../../integration-services/expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] デザイナーでこれらのプロパティを設定する方法については、次のトピックを参照してください。  
  
-   [タスクまたはコンテナーのプロパティを設定する](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>プログラムによるログイン転送タスクの構成  
 プログラムによってこれらのプロパティを設定する方法の詳細については、次のトピックを参照してください。  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
## <a name="transfer-logins-task-editor-general-page"></a>[ログイン転送タスク エディター] ([全般] ページ)
  **[ログイン転送タスク エディター]** ダイアログ ボックスの **[全般]** ページを使用すると、ログイン転送タスクの名前と説明を入力します。  
  
### <a name="options"></a>オプション  
 **[名前]**  
 ログイン転送タスクの一意の名前を入力します。 この名前は、タスク アイコンのラベルとして使用されます。  
  
> [!NOTE]  
>  タスク名はパッケージ内で一意である必要があります。  
  
 **[説明]**  
 ログイン転送タスクの説明を入力します。  
  
## <a name="transfer-logins-task-editor-logins-page"></a>[ログイン転送タスク エディター] ([ログイン] ページ)
  **[ログイン転送タスク エディター]** ダイアログ ボックスの **[ログイン]** ページを使用すると、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスから別のインスタンスへと [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインをコピーする際のプロパティを指定できます。  
  
> [!IMPORTANT]  
>  ログイン転送タスクを実行すると、転送先のサーバー上でランダムなパスワードを使用してログインが作成され、パスワードが無効になります。 このログインを使用するには、 **sysadmin** 固定サーバー ロールのメンバーでパスワードを変更し、そのパスワードを有効にする必要があります。 **sa** ログインは転送できません。  
  
### <a name="options"></a>オプション  
 **SourceConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー元のサーバーへの新しい接続を作成します。  
  
 **DestinationConnection**  
 SMO 接続マネージャーを一覧から選択するか、 **\<[新しい接続...]>** をクリックしてコピー先のサーバーへの新しい接続を作成します。  
  
 **[LoginsToTransfer]**  
 転送元サーバーから転送先サーバーにコピーされる [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインを選択します。 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[AllLogins]**|転送元サーバーのすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインが転送先サーバーにコピーされます。|  
|**[SelectedLogins]**|**[LoginsList]** に指定されているログインのみが転送先サーバーにコピーされます。|  
|**[AllLoginsFromSelectedDatabases]**|**[DatabasesList]** で指定されているデータベース内のすべてのログインが転送先サーバーにコピーされます。|  
  
 **[LoginsList]**  
 転送先サーバーにコピーする、転送元サーバーのログインを選択します。 このオプションは、 **[LoginsToTransfer]** を **[SelectedLogins]** に設定した場合のみ使用できます。  
  
 **[DatabasesList]**  
 転送先サーバーにコピーするログインが含まれる、転送元サーバー上のデータベースを選択します。 このオプションは、 **[LoginsToTransfer]** を **[AllLoginsFromSelectedDatabases]** に設定した場合のみ使用できます。  
  
 **[IfObjectExists]**  
 転送先サーバーに同じ名前のログインが既に存在していた場合の処理方法を選択します。  
  
 このプロパティには、次の表に示すオプションがあります。  
  
|[値]|[説明]|  
|-----------|-----------------|  
|**[FailTask]**|転送先サーバーに同じ名前のログインが既に存在していた場合、タスクが失敗します。|  
|**Overwrite**|転送先サーバーにある同じ名前のログインは上書きされます。|  
|**Skip**|転送先サーバーにある同じ名前のログインはスキップされます。|  
  
 **[CopySids]**  
 ログインに関連付けられたセキュリティ識別子を転送先サーバーにコピーするかどうかを選択します。 ログイン転送タスクをデータベース転送タスクと同時に使用する場合、 **[CopySids]** を **[True]** に設定する必要があります。 そのように設定しなかった場合、コピーされたログインは転送されたデータベースで認識されなくなります。  
  
