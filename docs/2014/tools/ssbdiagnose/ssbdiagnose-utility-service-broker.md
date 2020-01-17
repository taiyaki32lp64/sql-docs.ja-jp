---
title: ssbdiagnose ユーティリティ (Service Broker) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- Service Broker, runtime reports
- Service Broker, command prompt utilities
- troubleshooting [Service Broker], conversations
- troubleshooting [Service Broker], configurations
- command prompt utilities [Service Broker]
- Service Broker, troubleshooting
- Service Broker, configuration reports
- Service Broker, tools
- troubleshooting [Service Broker], runtime
- conversations [Service Broker], troubleshooting
- troubleshooting [Service Broker], ssbdiagnose utility
- tools [Service Broker], ssbdiagnose
- Service Broker, ssbdiagnose utility
- ssbdiagnose
ms.assetid: 0c1636e8-a3db-438e-be4c-1ea40d1f4877
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 323ccf41b5285f4bc395223025ea164a330c28a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211004"
---
# <a name="ssbdiagnose-utility-service-broker"></a>ssbdiagnose ユーティリティ (Service Broker)
  **ssbdiagnose** ユーティリティは、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換または [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスの構成に関する問題を報告します。 構成チェックは 2 つまたは 1 つのサービスに対して実行できます。 問題点は、コマンド プロンプト ウィンドウにユーザーが解釈できる形式で報告されるか、ファイルまたは別のプログラムにリダイレクトできる XML 形式で報告されます。  
  
## <a name="syntax"></a>構文  
  
```  
  
      ssbdiagnose   
[ [ -XML ]  
    [ -LEVEL { ERROR | WARNING | INFO } ]  
  [-IGNOREerror_id ] [ ...n]  
    [ <baseconnectionoptions> ]  
  { <configurationreport> | <runtimereport> }  
]  
| -?  
  
<configurationreport> ::=  
    CONFIGURATION  
  { [ FROM SERVICEservice_name  
      [ <fromconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
    [ TO SERVICEservice_name[, broker_id ]  
      [ <toconnectionoptions> ]  
      [ MIRROR <mirrorconnectionoptions> ]  
    ]  
  }  
    ON CONTRACTcontract_name  
  [ ENCRYPTION { ON | OFF | ANONYMOUS } ]  
  
<runtime_report> ::=  
    RUNTIME  
    [-SHOWEVENTS ]  
        [ -NEW  
         [ -ID { conversation_handle  
                | conversation_group_id  
                 | conversation_id  
                  }  
        ] [ ...n]  
        ]  
    [ -TIMEOUTtimeout_interval ]  
    [ <runtimeconnectionoptions> ]  
  
<baseconnectionoptions> ::=  
  <connectionoptions>  
  
<fromconnectionoptions> ::=  
  <connectionoptions>  
  
<toconnectionoptions> ::=  
  <connectionoptions>  
  
<mirrorconnectionoptions> ::=  
  <connectionoptions>  
  
<runtimeconnectionoptions> ::=  
  [ CONNECT TO <connectionoptions> ] [ ...n]  
  
<connectionoptions> ::=  
    [ -E | { -Ulogin_id [ -Ppassword ] } ]  
  [ -Sserver_name[\instance_name] ]  
  [ -ddatabase_name ]  
  [ -llogin_timeout ]  
  
```  
  
## <a name="command-line-options"></a>コマンド ライン オプション  
 **-XML**  
 **ssbdiagnose** の出力を XML 形式で生成することを指定します。 この出力は、ファイルまたは他のアプリケーションにリダイレクトできます。 **-XML** が指定されていない場合は、 **ssbdiagnose** の出力がユーザーが解釈できる形式に設定されます。  
  
 **-LEVEL** { **ERROR** | **WARNING** | **INFO**}  
 報告するメッセージのレベルを指定します。  
  
 **ERROR**: エラー メッセージのみを報告します。  
  
 **WARNING**: エラー メッセージと警告メッセージを報告します。  
  
 **INFO**: エラー メッセージ、警告メッセージ、および情報メッセージを報告します。  
  
 既定の設定は **WARNING**です。  
  
 **-IGNORE** *error_id*  
 指定した *error_id* のエラーまたはメッセージがレポートから除外されます。 **-IGNORE** を複数回指定すると、複数のメッセージ ID を除外することができます。  
  
 **\<baseconnectionoptions>**  
 接続オプションが特定の句に含まれていない場合に **ssbdiagnose** が使用する、基本的な接続情報を指定します。 特定の句で指定された接続情報は、**baseconnectionoption** の情報をオーバーライドします。 優先的に使用される接続情報は、パラメーターごとに判別されます。 たとえば、 **-S** と **-d** の両方が **baseconnetionoptions**で指定され、 **-d** のみが **toconnetionoptions**で指定されている場合、 **ssbdiagnose** では、 **baseconnetionoptions** の -S と **toconnetionoptions**の -d が使用されます。  
  
 **CONFIGURATION**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスのペアまたは 1 つのサービスでの構成エラーのレポートを要求します。  
  
 **FROM SERVICE** *service_name*  
 メッセージ交換を開始するサービスを指定します。  
  
 **\<fromconnectionoptions>**  
 発信側サービスが格納されているデータベースへの接続に必要な情報を指定します。 **fromconnectionoptions** が指定されていない場合、 **ssbdiagnose** では **baseconnectionoptions** の接続情報を使用して発信側データベースに接続します。 **fromconnectionoptions** が指定されている場合は、発信側サービスが格納されているデータベースを含める必要があります。 **fromconnectionoptions** が指定されていない場合は、 **baseconnectionoptions** で発信側データベースを指定する必要があります。  
  
 **TO SERVICE** *service_name*[, *broker_id* ]  
 メッセージ交換の発信先サービスを指定します。  
  
 *service_name*: 発信先サービスの名前を指定します。  
  
 *broker_id*: 発信先データベースを示す [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID を指定します。 *broker_id* は GUID です。 発信先データベースで次のクエリを実行すると、この ID を検索できます。  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 **\<toconnectionoptions>**  
 発信先サービスが格納されているデータベースへの接続に必要な情報を指定します。 **toconnectionoptions** が指定されていない場合、 **ssbdiagnose** では **baseconnectionoptions** の接続情報を使用して発信先データベースに接続します。  
  
 **MIRROR**  
 関連する [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスが、ミラー化されたデータベースでホストされます。 **ssbdiagnose** は、サービスへのルートがミラー化されたルートであることを確認します。この場合、MIRROR_ADDRESS が CREATE ROUTE で指定されています。  
  
 **\<mirrorconnectionoptions>**  
 ミラー データベースへの接続に必要な情報を指定します。 **mirrorconnectionoptions** が指定されていない場合、 **ssbdiagnose** では **baseconnectionoptions** の接続情報を使用してミラー データベースに接続します。  
  
 **ON CONTRACT** *contract_name*  
 指定されたコントラクトを使用する構成のみを **ssbdiagnose** でチェックするように要求します。 ON CONTRACT が指定されていない場合、 **ssbdiagnose** では、DEFAULT という名前のコントラクトに関するレポートが生成されます。  
  
 **ENCRYPTION** { **ON** | **OFF** | **ANONYMOUS** }  
 指定されたレベルの暗号化向けにダイアログが正しく構成されているかどうかを検証するように要求します。  
  
 **ON**:既定の設定 完全ダイアログ セキュリティが構成されているかどうかを検証します。 証明書がダイアログの両側に配置されていること、リモート サービス バインドが存在すること、および発信先サービスに対する GRANT SEND ステートメントで発信側ユーザーを指定していることを確認します。  
  
 **OFF**:ダイアログ セキュリティが構成されていないかどうかを検証します。 証明書が配置されていないこと、リモート サービス バインドが作成されていないこと、および発信側サービスに対する GRANT SEND ステートメントで **public** ロールを指定していることを確認します。  
  
 **ANONYMOUS**:匿名ダイアログ セキュリティが構成されているかどうかを検証します。 一方の証明書が配置されていること、リモート サービス バインドで匿名句が指定されていること、および発信先サービスに対する GRANT SEND ステートメントで **public** ロールを指定していることを確認します。  
  
 **RUNTIME**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] メッセージ交換の実行時エラーの原因である問題に関するレポートを要求します。 **-NEW** も **-ID** も指定されていない場合、 **ssbdiagnose** では、接続オプションで指定されたすべてのデータベース内のメッセージ交換をすべて監視します。 **-NEW** または **-ID** が指定されている場合、**ssbdiagnose** では、パラメーターで指定された ID の一覧が作成されます。  
  
 **ssbdiagnose[!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] は、実行中に、実行時エラーを示す**  イベントをすべて記録します。 また、指定された ID に対して発生するイベントに加え、システムレベルのイベントも記録します。 実行時エラーが検出されると、 **ssbdiagnose** では、関連付けられている構成に対して構成レポートを実行します。  
  
 既定では、出力レポートに実行時エラーは含まれず、構成の分析結果のみが含まれます。 レポートに実行時エラーを含めるには、 **-SHOWEVENTS** を使用してください。  
  
 **-SHOWEVENTS**  
 **ssbdiagnose** で RUNTIME レポートの実行中に [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] イベントを報告するように指定します。 エラー状態と見なされるイベントのみが報告されます。 既定では、 **ssbdiagnose** はエラー イベントを監視するだけで、エラー イベントをレポートに出力しません。  
  
 **-NEW**  
 **ssbdiagnose** が実行を開始した後に開始される最初のメッセージ交換を、実行時に監視するように要求します。  
  
 **-ID**  
 指定されたメッセージ交換要素を実行時に監視するように要求します。 **-ID** は複数回指定できます。  
  
 メッセージ交換ハンドルを指定すると、関連するメッセージ交換のエンドポイントに関連付けられたイベントのみが報告されます。 メッセージ交換 ID を指定すると、そのメッセージ交換のすべてのイベントと、そのメッセージ交換の発信側と発信先のエンドポイントが報告されます。 メッセージ交換グループ ID が指定されている場合は、すべてのメッセージ交換のイベントと、メッセージ交換グループ内のエンドポイントが報告されます。  
  
 *conversation_handle*  
 アプリケーション内のメッセージ交換エンドポイントを識別する一意識別子です。 メッセージ交換ハンドルは、メッセージ交換の一方のエンドポイントに対して一意であり、発信側と発信先のエンドポイントのメッセージ交換ハンドルは異なります。  
  
 によって、アプリケーションにメッセージ交換ハンドルが返されます、 *@dialog_handle* のパラメーター、 **BEGIN DIALOG**ステートメントでは、および`conversation_handle`の結果の列のセットを**受信**ステートメント。  
  
 メッセージ交換ハンドルで報告される、`conversation_handle`の列、 **sys.transmission_queue**と**sys.conversation_endpoints**カタログ ビューです。  
  
 *conversation_group_id*  
 メッセージ交換グループを識別する一意識別子です。  
  
 によって、アプリケーションにメッセージ交換グループ Id が返されます、 *@conversation_group_id* のパラメーター、 **GET CONVERSATION GROUP**ステートメントおよび`conversation_group_id`の結果セット内の列**受信**ステートメント。  
  
 メッセージ交換グループ Id が報告、`conversation_group_id`の列、 **sys.conversation_groups**と**sys.conversation_endpoints**カタログ ビューです。  
  
 *conversation_id*  
 メッセージ交換を識別する一意識別子です。 メッセージ交換 ID は、メッセージ交換の発信側と発信先の両方のエンドポイントで同じです。  
  
 メッセージ交換 Id が報告、`conversation_id`の列、 **sys.conversation_endpoints**カタログ ビューです。  
  
 **-TIMEOUT** *timeout_interval*  
 **RUNTIME** レポートを実行する秒数を指定します。 **-TIMEOUT** が指定されていない場合、ランタイム レポートは無制限に実行されます。 **-TIMEOUT** は、**CONFIGURATION** レポートではなく、**RUNTIME** レポートのみで使用されます。 **-TIMEOUT** が指定されていない場合に **ssbdiagnose** を終了したり、タイムアウト間隔を経過する前にランタイム レポ **-** トを終了したりするには、Ctrl キーを押しながら C キーを押します。 *timeout_interval* は 1 から 2,147,483,647 までの数値にする必要があります。  
  
 **\<runtimeconnectionoptions>**  
 監視対象のメッセージ交換要素に関連付けられたサービスが格納されているデータベースについての接続情報を指定します。 すべてのサービスが同じデータベースに格納されている場合は、 **CONNECT TO** 句を 1 つ指定するだけで十分です。 サービスが異なるデータベースに格納されている場合は、各データベースに対して **CONNECT TO** 句を指定する必要があります。 **runtimeconnectionoptions** が指定されていない場合、 **ssbdiagnose** では **baseconnectionoptions**の接続情報を使用します。  
  
 **-E**  
 現在の Windows アカウントをログイン ID として使用して、 [!INCLUDE[ssDE](../../includes/ssde-md.md)] のインスタンスに対して Windows 認証接続を開きます。 ログインは **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
 -E オプションを使用すると、SQLCMDUSER 環境変数および SQLCMDPASSWORD 環境変数のユーザー設定とパスワード設定が無視されます。  
  
 **-E** も **ｰU** も指定されていない場合、 **ssbdiagnose** では、SQLCMDUSER 環境変数の値を使用します。 SQLCMDUSER も設定されていない場合、 **ssbdiagnose** では Windows 認証を使用します。  
  
 **-E** オプションが **-U** オプションまたは **-P** オプションと共に使用されると、エラー メッセージが生成されます。  
  
 **ｰU** *login_id*  
 指定されたログイン ID を使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証接続を開きます。 ログインは **sysadmin** 固定サーバー ロールのメンバーである必要があります。  
  
 **-E** も **ｰU** も指定されていない場合、 **ssbdiagnose** では、SQLCMDUSER 環境変数の値を使用します。 SQLCMDUSER も設定されていない場合、 **ssbdiagnose** では、 **ssbdiagnose**を実行しているユーザーの Windows アカウントに基づいた Windows 認証モードを使用して接続を試行します。  
  
 **-U** オプションを **-E** オプションと共に使用すると、エラー メッセージが生成されます。 **-U** オプションの後に複数の引数があると、エラー メッセージが生成され、プログラムが終了します。  
  
 **-P** *password*  
 **-U** ログイン ID のパスワードを指定します。 パスワードでは大文字と小文字が区別されます。 **-U** オプションが使用され、 **-P** オプションが使用されていない場合、 **ssbdiagnose** では、SQLCMDPASSWORD 環境変数の値を使用します。 SQLCMDPASSWORD も設定されていない場合は、 **ssbdiagnose** はユーザーにパスワードを要求します。  
  
> [!IMPORTANT]  
>  SET SQLCMDPASSWORD コマンドを入力する際は、モニターにパスワードが表示されてしまうので注意してください。  
  
 パスワードなしで **-P** オプションが指定されている場合、 **ssbdiagnose** では既定のパスワード (NULL) を使用します。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] 詳細については、「 [Strong Passwords](../../relational-databases/security/strong-passwords.md)」を参照してください。  
  
 パスワード プロンプトは、次のようにパスワード プロンプトをコンソールに出力することによって表示されます。 `Password:`  
  
 ユーザーが行った入力は表示されません。 つまり、入力時には何も表示されず、カーソルが移動しません。  
  
 **-P** オプションが **-E** オプションと共に使用されると、エラー メッセージが生成されます。  
  
 **-P** オプションに複数の引数がある場合は、エラー メッセージが生成されます。  
  
 **-S** *server_name*[\\*instance_name*]  
 分析対象の [!INCLUDE[ssDE](../../includes/ssde-md.md)] サービスが格納されている、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] のインスタンスを指定します。  
  
 サーバー上の *の既定のインスタンスに接続するには、* server_name [!INCLUDE[ssDE](../../includes/ssde-md.md)] を指定します。 サーバー上の [!INCLUDE[ssDE](../../includes/ssde-md.md)]の名前付きインスタンスに接続するには、*server_name***\\***instance_name* を指定します。 **-S** が指定されていない場合、 **ssbdiagnose** では、SQLCMDSERVER 環境変数の値を使用します。 SQLCMDSERVER も設定されていない場合、 **ssbdiagnose** はローカル コンピューター上にある [!INCLUDE[ssDE](../../includes/ssde-md.md)] の既定のインスタンスに接続します。  
  
 **-d** *database_name*  
 分析対象の [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスが格納されているデータベースを指定します。 データベースが存在しない場合は、エラー メッセージが生成されます。 **-d** が指定されていない場合、ログインの既定のデータベースのプロパティに指定されたデータベースが既定値になります。  
  
 **-l** *login_timeout*  
 サーバーへの接続試行がタイムアウトするまでの秒数を指定します。 **-l** が指定されていない場合、 **ssbdiagnose** では、SQLCMDLOGINTIMEOUT 環境変数に設定された値を使用します。 SQLCMDLOGINTIMEOUT も設定されていない場合、既定のタイムアウトは 30 秒です。 ログイン タイムアウトは、0 ～ 65,534 の数値にする必要があります。 指定した値が数値以外の場合、または範囲外の場合、 **ssbdiagnose** はエラー メッセージを生成します。 この値に 0 を指定すると、タイムアウトは無制限になります。  
  
 **-?**  
 コマンド ライン ヘルプを表示します。  
  
## <a name="remarks"></a>コメント  
 **ssbdiagnose** を使用すると、次の操作を実行できます。  
  
-   新しく構成された [!INCLUDE[ssSB](../../includes/sssb-md.md)] アプリケーションに構成エラーがないことを確認する。  
  
-   既存の [!INCLUDE[ssSB](../../includes/sssb-md.md)] アプリケーションの構成を変更した後に構成エラーがないことを確認する。  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] データベースをデタッチしてから [!INCLUDE[ssDE](../../includes/ssde-md.md)]のインスタンスに再アタッチした後に構成エラーがないことを確認する。  
  
-   メッセージがサービス間で正常に送信されない場合に構成エラーがあるかどうかを調査する。  
  
-   [!INCLUDE[ssSB](../../includes/sssb-md.md)] の一連のメッセージ交換要素で発生するすべてのエラーに関するレポートを取得する。  
  
## <a name="configuration-reporting"></a>構成レポート  
 メッセージ交換で使用されている構成を正しく分析するには、メッセージ交換で使用されているオプションと同じオプションを使用する **ssbdiagnose** の構成レポートを実行します。 メッセージ交換よりも低いレベルのオプションを **ssbdiagnose** に指定すると、 **ssbdiagnose** は、メッセージ交換に必要な条件を報告しない場合があります。 また、より高いレベルのオプションを **ssbdiagnose**に指定すると、メッセージ交換に必要のない項目を報告する場合があります。 たとえば、同じデータベース内の 2 つのサービス間のメッセージ交換は、ENCPRYPTION OFF を指定して実行できます。 **ssbdiagnose** を実行してこの 2 つのサービス間の構成を検証する場合でも、既定の設定 ENCRYPTION ON を使用すると、 **ssbdiagnose** は、データベースにマスター キーが存在しないことを報告します。 マスター キーは、メッセージ交換には必要ありません。  
  
 **ssbdiagnose** の構成レポートを実行するたびに、1 つの [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスまたは 1 組のサービスが分析されます。 [!INCLUDE[ssSB](../../includes/sssb-md.md)] サービスの複数のペアに関するレポートを作成するには、 **ssbdiagnose** を複数回呼び出す .cmd コマンド ファイルを作成します。  
  
## <a name="runtime-reporting"></a>ランタイム レポート  
 -RUNTIME が指定されている場合、 **ssbdiagnose** は **runtimeconnectionoptions** と **baseconnectionoptions** で指定されたすべてのデータベースを検索して、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID の一覧を作成します。 作成される ID の一覧は、-NEW および -ID で指定する内容によって異なります。  
  
-   **-NEW** も **-ID** も指定されていない場合、接続オプションで指定されたすべてのデータベースに関するすべてのメッセージ交換が一覧に含まれます。  
  
-   **-NEW** が指定されている場合、 **ssbdiagnose** が作成する一覧には、 **ssbdiagnose** の実行後に開始される最初のメッセージ交換の要素が含まれます。 これには、メッセージ交換 ID、および発信先と発信側の両方のメッセージ交換エンドポイントのメッセージ交換ハンドルも含まれます。  
  
-   **-ID** がメッセージ交換ハンドルと共に指定されている場合、そのハンドルのみが一覧に含まれます。  
  
-   **-ID** がメッセージ交換 ID と共に指定されている場合、そのメッセージ交換 ID と、そのメッセージ交換の両方のエンドポイントのハンドルが一覧に追加されます。  
  
-   **-ID** がメッセージ交換グループ ID と共に指定されている場合、そのグループ内のすべてのメッセージ交換 ID とメッセージ交換ハンドルが一覧に追加されます。  
  
 接続オプションで対応されていないデータベースの要素は、一覧に含まれません。 たとえば、 **-ID** を使用してメッセージ交換 ID を指定しても、発信先データベースではなく発信側データベースのみに対して **runtimeconnectionoptions** 句を指定するとします。 **ssbdiagnose** は、発信先のメッセージ交換ハンドルを ID の一覧に含めず、メッセージ交換 ID と、発信側のメッセージ交換ハンドルのみを含めます。  
  
 **ssbdiagnose** では、 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] runtimeconnectionoptions **と** baseconnectionoptions **に含まれるデータベースの**イベントを監視します。 この ssbdiagnose は、ランタイムの一覧に含まれる 1 つ以上の [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID でエラーが発生したことを示す [!INCLUDE[ssSB](../../includes/sssb-md.md)] イベントを検索します。 また、**ssbdiagnose** は、どのメッセージ交換グループにも特に関連付けられていないシステムレベルの [!INCLUDE[ssSB](../../includes/sssb-md.md)] エラー イベントも検索します。  
  
 **ssbdiagnose** がメッセージ交換エラーを検出すると、このユーティリティは、構成レポートも実行して、そのイベントの根本的な原因の報告を試行します。 **ssbdiagnose** では、データベース内のメタデータを使用して、メッセージ交換で使用されるインスタンス、 [!INCLUDE[ssSB](../../includes/sssb-md.md)] ID、データベース、サービス、およびコントラクトを特定します。 その後、使用可能なすべての情報を使用して構成レポートを実行します。  
  
 既定では、 **ssbdiagnose** はエラー イベントを報告しません。 報告するのは、構成チェック時に見つかった根本的な問題だけです。 これにより、報告される情報量が最小限に抑えられるため、根本的な構成の問題に注目することができます。 **-SHOWEVENTS** によって検出されたエラー イベントを確認するには、 **ssbdiagnose**を指定します。  
  
## <a name="issues-reported-by-ssbdiagnose"></a>ssbdiagnose によって報告される問題  
 **ssbdiagnose** が報告する問題は、3 種類に分類されます。 XML 出力ファイルでは、各種類の問題が Issue 要素の異なる型として報告されます。 **ssbdiagnose** が報告する 3 種類の問題は次のとおりです。  
  
 **診断**  
 構成上の問題を報告します。 これには、 **CONFIGURATION** レポートの実行中または **RUNTIME** レポートの構成フェーズ中に見つかった問題が含まれます。 **ssbdiagnose** は、構成上の各問題を一度だけ報告します。  
  
 **イベント**  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] RUNTIME **レポートの実行中に監視されるメッセージ交換で問題が検出されたことを示す** イベントを報告します。 **ssbdiagnose** は、イベントが生成されるたびにイベントを報告します。 複数のメッセージ交換で問題が検出される場合は、イベントが複数回報告されます。  
  
 **問題**  
 **ssbdiagnose** で構成分析を完了したり、メッセージ交換を監視したりすることができない場合に、その原因となる問題を報告します。  
  
## <a name="sqlcmd-environment-variables"></a>sqlcmd 環境変数  
 **ssbdiagnose** ユーティリティでは、 **sqlcmd** ユーティリティでも使用されている SQLCMDSERVER、SQLCMDUSER、SQLCMDPASSWORD、および SQLCMDLOGINTIMOUT の各環境変数がサポートされています。 これらの環境変数を設定するには、コマンド プロンプトの SET コマンドを使用するか、 **sqlcmd** を使用して実行する [!INCLUDE[tsql](../../includes/tsql-md.md)] スクリプトの **setvar**コマンドを使用します。 **sqlcmd** で **setvar**を使用する方法の詳細については、「 [sqlcmd でのスクリプト変数の使用](../../relational-databases/scripting/sqlcmd-use-with-scripting-variables.md)」をご覧ください。  
  
## <a name="permissions"></a>アクセス許可  
 各 **connectionoptions** 句では、 **-E** または **-U** のいずれかで指定されたログインが、 **-S** で指定されたインスタンスの **sysadmin**固定サーバー ロールのメンバーである必要があります。  
  
## <a name="examples"></a>使用例  
 ここでは、コマンド プロンプトでの **ssbdiagnose** の使用例を示します。  
  
### <a name="a-checking-the-configuration-of-two-services-in-the-same-database"></a>A. 同じデータベース内の 2 つのサービスの構成を確認する  
 次の例では、以下の条件に該当する場合に構成レポートを要求する方法を示します。  
  
-   発信側と発信先のサービスが同じデータベース内に格納されている。  
  
-   データベースが [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスに存在する。  
  
-   インスタンスが **ssbdiagnose** が実行されるコンピューター上に存在する。  
  
 ON CONTRACT が指定されていないため、 **ssbdiagnose** ユーティリティは、DEFAULT コントラクトを使用する構成を報告します。  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target  
```  
  
### <a name="b-checking-the-configuration-of-two-services-on-separate-computers-that-use-one-login"></a>B. 異なるコンピューター上の、同じログインを使用する 2 つのサービスの構成を確認する  
 次の例では、異なるコンピューター上に発信側と発信先のサービスが格納されており、そのサービスに同じ Windows 認証ログインを使用してアクセスできる場合に、構成レポートを要求する方法を示します。  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator -S InitiatorComputer -d InitiatorDatabase TO SERVICE /test/target -S TargetComputer -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="c-checking-the-configuration-of-two-services-on-separate-computers-that-use-separate-logins"></a>C. 異なるコンピューター上の、個別のログインを使用する 2 つのサービスの構成を確認する  
 次の例では、異なるコンピューター上に発信側と発信先のサービスが格納されており、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各インスタンスに個別の [!INCLUDE[ssDE](../../includes/ssde-md.md)]認証ログインが必要となる場合に、構成レポートを要求する方法を示します。  
  
```  
ssbdiagnose CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -U InitiatorLogin -p !wEx23Dvb   
-d InitiatorDatabase TO SERVICE /test/target -S TargetComputer   
-U TargetLogin -p ER!49jiy -d TargetDatabase ON CONTRACT TestContract  
```  
  
### <a name="d-checking-mirrored-service-configurations-on-separate-computers-with-anonymous-encryption"></a>D. 匿名の暗号化を使用している、異なるコンピューター上でミラー化されたサービスの構成を確認する  
 次の例では、異なるコンピューター上に発信側と発信先のサービスが格納されており、発信側が名前付きインスタンスにミラー化されている場合に、構成レポートを要求する方法を示します。 このレポートでは、サービスが匿名の暗号化を使用するように構成されていることも確認します。  
  
```  
ssbdiagnose -E CONFIGURATION FROM SERVICE /text/initiator   
-S InitiatorComputer -d InitiatorDatabase MIRROR   
-S MirrorComputer/MirrorInstance TO SERVICE /test/target   
-S TargetComputer -d TargetDatabase ON CONTRACT TestContract ENCRYPTION ANONYMOUS  
```  
  
### <a name="e-checking-the-configuration-of-two-contracts"></a>E. 2 つのコントラクトの構成を確認する  
 次の例では、以下の条件に該当する場合に構成レポートを要求するコマンド ファイルの作成方法を示します。  
  
-   発信側と発信先のサービスが同じデータベース内に格納されている。  
  
-   データベースが [!INCLUDE[ssDE](../../includes/ssde-md.md)]の既定のインスタンスに存在する。  
  
-   インスタンスが **ssbdiagnose** が実行されるコンピューター上に存在する。  
  
 **ssbdiagnose** は、実行されるたびに、同じサービス間で異なるコントラクトの構成を報告します。  
  
```  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target ON CONTRACT PayRaiseContract  
ssbdiagnose -E -d MyDatabase CONFIGURATION FROM SERVICE /test/initiator   
TO SERVICE /test/target ON CONTRACT PromotionContract  
```  
  
### <a name="f-monitor-the-status-of-a-specific-conversation-on-the-local-computer-with-a-time-out"></a>F. タイムアウトが設定された、ローカル コンピューター上の特定のメッセージ交換の状態を監視する  
 次の例では、 **ssbdiagnose**を実行しているコンピューターの既定のインスタンスにある同一のデータベースに発信側と発信先のサービスが格納されている場合に、特定のメッセージ交換を監視する方法を示します。 タイムアウト間隔は 20 秒に設定されています。  
  
```  
ssbdiagnose -E -d TestDatabase RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D -TIMEOUT 20  
```  
  
### <a name="g-monitor-the-status-of-a-conversation-that-spans-two-computers"></a>G. 2 台のコンピューターにまたがるメッセージ交換の状態を監視する  
 次の例では、異なるコンピューター上に発信側と発信先のサービスが格納されている場合に、特定のメッセージ交換を監視する方法を示します。  
  
```  
ssbdiagnose RUNTIME -ID D68D77A9-B1CF-41BF-A5CE-279ABCAB140D   
-TIMEOUT 10 CONNECT TO -E -S InitiatorComputer/InitiatorInstance   
-d InitiatorDatabase CONNECT TO -E -S TargetComputer/TargetInstance   
-d TargetDatabase  
```  
  
### <a name="h-monitor-the-status-of-a-conversation-in-two-databases-in-the-same-instance"></a>H. 同じインスタンス内の 2 つのデータベースにあるメッセージ交換の状態を監視する  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の同じインスタンスにある異なるデータベースに発信側と発信先のサービスが格納されている場合に、特定のメッセージ交換を監視する方法を示します。 この例では、 **baseconnectionoptions** を使用してインスタンスとログインの情報を指定し、2 つの CONNECT TO 句を使用してデータベースを指定しています。 すべてのランタイム イベントがレポートの出力に含まれるように、-SHOWEVENTS を指定しています。  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME -SHOWEVENTS   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="i-monitor-the-status-of-two-conversations-between-two-databases"></a>I. 2 つのデータベース間の 2 つのメッセージ交換の状態を監視する  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の同じインスタンスにある異なるデータベースに発信側と発信先のサービスが格納されている場合に、2 つのメッセージ交換を監視する方法を示します。 この例では、 **baseconnectionoptions** を使用してインスタンスとログインの情報を指定し、2 つの CONNECT TO 句を使用してデータベースを指定しています。  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-ID 5094d4a7-e38c-4c37-da37-1d58b1cb8455   
-ID 9b293be9-226b-4e22-e169-1d2c2c15be86 -TIMEOUT 10 CONNECT TO   
-d InitiatorDatabase CONNECT TO -d TargetDatabase  
```  
  
### <a name="j-monitor-the-status-of-all-conversations-between-two-databases"></a>J. 2 つのデータベース間のすべてのメッセージ交換の状態を監視する  
 次の例では、 [!INCLUDE[ssDE](../../includes/ssde-md.md)]の同じインスタンスにある 2 つのデータベース間で行われるすべてのメッセージ交換を監視する方法を示します。 この例では、 **baseconnectionoptions** を使用してインスタンスとログインの情報を指定し、2 つの CONNECT TO 句を使用してデータベースを指定しています。  
  
```  
ssbdiagnose -E -S TestComputer/DevTestInstance RUNTIME   
-TIMEOUT 10 CONNECT TO -d InitiatorDatabase CONNECT TO   
-d TargetDatabase  
```  
  
### <a name="k-ignore-specific-errors"></a>K. 特定のエラーを無視する  
 次の例では、テスト システムで現在アクティブ化を構成している方法で既知のエラー (303 と 304) を無視する方法を示します。  
  
```  
ssbdiagnose -IGNORE 303 -IGNORE 304 -E -d TestDatabase   
CONFIGURATION FROM SERVICE /test/initiator TO SERVICE /test/target   
ON CONTRACT TextContract  
```  
  
### <a name="l-redirecting-ssbdiagnose-xml-output"></a>L. ssbdiagnose の XML 出力をリダイレクトする  
 次の例では、 **ssbdiagnose** が出力を XML ファイルとして生成するように要求する方法を示します。この XML ファイルはファイルにリダイレクトされます。 その後、TestDiag.xml ファイルをアプリケーションで開いて、 **ssbdiagnose** の XML ファイルを分析およびレポートすることができます。 また、XML Notepad などの一般的な XML エディターで表示することもできます。  
  
```  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target > c:\MyDiagnostics\TestDiag.xml  
```  
  
### <a name="m-using-an-environment-variable"></a>M. 環境変数を使用する  
 次の例では、最初に、サーバー名を保持する SQLCMDSERVER 環境変数を設定し、次に、 **-S** を指定せずに **ssbdiagnose**を実行します。  
  
```  
SET SQLCMDSERVER=MyComputer  
ssbdiagnose -XML -E -d MyDatabase CONFIGURATION FROM SERVICE   
/test/initiator TO SERVICE /test/target  
```  
  
## <a name="see-also"></a>関連項目  
 [SQL Server Service Broker (SQL Server Service Broker)](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [BEGIN DIALOG CONVERSATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/begin-dialog-conversation-transact-sql)   
 [CREATE BROKER PRIORITY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-broker-priority-transact-sql)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)   
 [CREATE CONTRACT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-contract-transact-sql)   
 [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)   
 [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql)   
 [CREATE MESSAGE TYPE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-message-type-transact-sql)   
 [CREATE QUEUE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-queue-transact-sql)   
 [CREATE REMOTE SERVICE BINDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-remote-service-binding-transact-sql)   
 [CREATE ROUTE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-route-transact-sql)   
 [CREATE SERVICE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-service-transact-sql)   
 [RECEIVE &#40;Transact-SQL&#41;](/sql/t-sql/statements/receive-transact-sql)   
 [sys.transmission_queue &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-transmission-queue-transact-sql)   
 [sys.conversation_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-conversation-endpoints-transact-sql)   
 [sys.conversation_groups &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-conversation-groups-transact-sql)  
  
  
