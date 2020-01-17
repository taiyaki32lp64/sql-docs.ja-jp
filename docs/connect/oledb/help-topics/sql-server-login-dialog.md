---
title: '[ログインの SQL Server] ダイアログボックス (OLE DB) |Microsoft Docs'
description: '[SQL Server ログイン] ダイアログ ボックスの使用'
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d35c339798b4385cb903d8a4a83f13184bbf4db3
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381753"
---
# <a name="sql-server-login-dialog-box"></a>[SQL Server ログイン] ダイアログ ボックス
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

十分な情報を指定せずに接続しようとすると、OLE DB ドライバに **[SQL Server ログイン]** ダイアログボックスが表示されます。

> [!NOTE]  
> SQL Server ログインダイアログのプロンプト動作は、`DBPROP_INIT_PROMPT` 初期化プロパティによって制御されます。 詳細については、以下をご覧ください。
> - [初期化プロパティと承認プロパティ](../ole-db-data-source-objects/initialization-and-authorization-properties.md)
> - [OLE DB プログラマーガイド](https://go.microsoft.com/fwlink/?linkid=2067702)

![SQL Server ログインダイアログボックスのスクリーンショット](../media/sql-server-login-dialog.png)

## <a name="options"></a>オプション
|オプション|[説明]|
|---   |---        |
|[サーバー]|ネットワーク上の SQL Server のインスタンスの名前。 一覧から server\instance 形式の名前を選択するか、 **[サーバー]** ボックスに server\instance 形式の名前を入力します。 必要に応じて、**SQL Server 構成マネージャー**を使用してクライアント コンピューターでサーバーの別名を作成し、 **[サーバー]** ボックスにその名前を入力することができます。 <br/><br/>SQL Server と同じコンピューターを使用している場合は、「(local)」と入力することができます。 その後、ネットワークに接続されていない SQL Server を実行している場合でも、SQL Server のローカル インスタンスに接続することができます。<br/><br/>さまざまな種類のネットワークのサーバー名の詳細については、「 [SQL Server のインストール](https://go.microsoft.com/fwlink/?linkid=2067541)」を参照してください。|
|認証モード|ドロップダウンリストから、次の認証オプションを選択できます。<br/><ul><li>現在ログインしているユーザーの Windows アカウントの資格情報を使用して SQL Server する認証を `Windows Authentication:` します。</li><li>ログイン ID とパスワードを使用して認証を `SQL Server Authentication:` します。</li><li>Azure Active Directory id を使用して統合認証を `Active Directory - Integrated:` します。 このモードは、Windows 認証に SQL Server するためにも使用できます。</li><li>Azure Active Directory id を使用してユーザー ID とパスワード認証を `Active Directory - Password:` します。</li><li>Azure Active Directory id を使用した対話型認証を `Active Directory - Universal with MFA support:` します。 このモードでは、Azure multi-factor authentication (MFA) がサポートされます。</li></ul>|
|サーバー SPN|セキュリティ接続を使用する場合、サーバーのサービス プリンシパル名 (SPN) を指定できます。|
|Login ID|接続に使用するログイン ID を指定します。 [ログイン ID] ボックスは、`Authentication Mode` が `SQL Server Authentication`、`Active Directory - Password`、または `Active Directory - Universal with MFA support` に設定されている場合にのみ有効になります。|
|Password|接続に使用するパスワードを指定します。 [パスワード] テキストボックスは、`Authentication Mode` が `SQL Server Authentication` または `Active Directory - Password` に設定されている場合にのみ有効になります。|
|オプション|**[オプション]** グループを表示または非表示にします。 **[オプション]** ボタンは、 **[サーバー]** に値が設定されている場合に有効になります。|
|パスワードの変更|オンにすると、 **[新しいパスワード]** ボックスと **[新しいパスワードの確認]** 入力 ボックスが有効になります。|
|[新しいパスワード]|新しいパスワードを指定します。|
|[新しいパスワードの確認入力]|確認のために、新しいパスワードをもう一度指定します。|
|データベース|接続で使用する既定のデータベースを選択または入力します。 この設定は、サーバーのログインに指定されている既定のデータベースをオーバーライドします。 データベースが指定されていない場合、接続はサーバーのログインに指定されている既定のデータベースを使用します。|
|[ミラー サーバー]|ミラー化するデータベースのフェールオーバー パートナーの名前を指定します。|
|[ミラー SPN]|必要に応じて、ミラー サーバーに SPN を指定できます。 ミラー サーバーの SPN は、クライアントとサーバー間の相互認証に使用されます。|
|[言語]|SQL Server システム メッセージに使用する言語を指定します。 SQL Server を実行しているコンピューターには言語がインストールされている必要があります。 この設定は、サーバーのログインに指定されている既定の言語をオーバーライドします。 言語が指定されていない場合、接続はサーバーのログインに指定されている既定の言語を使用します。|
|Application Name|**sys.sysprocesses** 内でこの接続の行の **program_name** 列に格納されるアプリケーション名を指定します。|
|[ワークステーション ID]|**sys.sysprocesses** 内でこの接続の行の **hostname** 列に格納されるワークステーション ID を指定します。|
|[データに強力な暗号を使用する]|オンにすると、接続を介して渡されるデータが暗号化されます。|
|[サーバー証明書を信頼する]|オンにすると、サーバーの証明書が検証されます。 サーバーの証明書には、サーバーの正しいホスト名があり、信頼された証明機関によって発行されている必要があります。|

> [!NOTE]  
> @No__t_0 モードまたは `SQL Server Authentication` モードを使用する場合、[**データの強力な暗号化を使用**する] オプションが有効になっている場合にのみ、**信頼サーバー証明書**が考慮されます。

## <a name="next-steps"></a>次の手順
- OLE DB ドライバーを使用して[Azure Active Directory に対する認証を](../features/using-azure-active-directory.md)行います。
- [ユニバーサルデータリンク (UDL)](data-link-pages.md)を使用して接続情報を設定します。