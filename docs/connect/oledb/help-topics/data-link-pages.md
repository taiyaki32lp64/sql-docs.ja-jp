---
title: ユニバーサルデータリンク (UDL) の構成 |Microsoft Docs
description: Microsoft OLE DB Driver for SQL Server を使用したユニバーサルデータリンク (UDL) の構成
ms.custom: ''
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
ms.author: v-beaziz
author: bazizi
ms.openlocfilehash: d92555fba1d9e0a380ffdc9051817ddfae9ca4b7
ms.sourcegitcommit: 4c75b49599018124f05f91c1df3271d473827e4d
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72381760"
---
# <a name="universal-data-link-udl-configuration"></a>ユニバーサル データ リンク (UDL) の構成
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

## <a name="connection-tab"></a>[接続] タブ
Microsoft OLE DB Driver for SQL Server を使用してデータに接続する方法を指定するには、[接続] タブを使用します。

![OLE DB データリンクページのスクリーンショット-[接続] タブ](../media/data-link-pages-connection-tab.png)

[接続] タブはプロバイダー固有であり、Microsoft OLE DB Driver for SQL Server に必要な接続プロパティだけが表示されます。

|オプション|[説明]|
|---   |---        |
|[サーバー名の選択または入力]|ドロップダウン リストからサーバー名を選択するか、アクセスするデータベースが格納されているサーバーの場所を入力します。 サーバー上のデータベースを選択するのは別の操作です。 一覧を更新するには、"更新" をクリックします。
|サーバーにサインインするための情報を入力してください|このドロップダウンリストからは、次の認証オプションを選択できます。 <ul><li>現在ログインしているユーザーの Windows アカウントの資格情報を使用して SQL Server する認証を `Windows Authentication:` します。</li><li>ログイン ID とパスワードを使用して認証を `SQL Server Authentication:` します。</li><li>Azure Active Directory id を使用して統合認証を `Active Directory - Integrated:` します。 このモードは、Windows 認証に SQL Server するためにも使用できます。</li><li>Azure Active Directory id を使用してユーザー ID とパスワード認証を `Active Directory - Password:` します。</li><li>Azure Active Directory id を使用した対話型認証を `Active Directory - Universal with MFA support:` します。 このモードでは、Azure multi-factor authentication (MFA) がサポートされます。</li></ul>|
|サーバー SPN|セキュリティ接続を使用する場合、サーバーのサービス プリンシパル名 (SPN) を指定できます。|
|[ユーザー名]|データソースにサインインするときに認証に使用するユーザー ID を入力します。|
|Password|データソースにサインインするときに認証に使用するパスワードを入力します。|
|パスワードを空白にする|オンにすると、指定したプロバイダーが接続文字列で空白のパスワードを使用できるようになります。|
|パスワードを保存する|オンにすると、接続文字列と共にパスワードを保存できるようになります。 パスワードが接続文字列に含まれるかどうかは、呼び出し元アプリケーションの機能によって決まります。 <br/><br/>**注:** 保存する場合、パスワードはマスクも暗号化もされない状態で返されて保存されます。|
|[データに強力な暗号を使用する]|オンにすると、接続を介して渡されるデータが暗号化されます。|
|[サーバー証明書を信頼する]|オンにすると、サーバーの証明書が検証されます。 サーバーの証明書には、サーバーの正しいホスト名があり、信頼された証明機関によって発行されている必要があります。|
|データベースを選択する|アクセスするデータベース名を選択または入力します。|
|データベース ファイルをデータベース名として添付する|アタッチできるデータベースのプライマリ ファイルの名前を指定します。 このデータベースがアタッチされ、データ ソースの既定のデータベースとして使用されます。 このセクションの最初のテキストボックスに、アタッチされたデータベースファイルに使用するデータベース名を入力します。<br/><br/>@No__t_0 ラベルが付けられたデータベースファイルへの完全パスを入力します。または、[`...`] ボタンをクリックしてデータベースファイルを参照します。|
|パスワードの変更|パスワード変更の SQL Server ダイアログを表示します。 |
|[接続テスト]|指定したデータソースへの接続を試行する場合にクリックします。 接続に失敗した場合、設定が正しいかどうかを確認します。 たとえば、スペル ミスや大文字と小文字の区別は接続の失敗の原因になる場合があります。|

## <a name="advanced-tab"></a>[詳細設定] タブ
[詳細設定] タブを使用すると、追加の初期化プロパティを表示および設定できます。

![OLE DB データリンクページのスクリーンショット-[詳細設定] タブ](../media/data-link-pages-advanced-tab.png)

|オプション|[説明]|
|---   |---        |
| 接続のタイムアウト | Microsoft OLE DB Driver for SQL Server が初期化の完了を待機する時間 (秒) を指定します。 初期化がタイムアウトすると、エラーが返され、接続は作成されません。|


> [!NOTE]  
>  一般的なデータリンクの接続情報については、「[データリンク API の概要](https://go.microsoft.com/fwlink/?linkid=2067432)」を参照してください。

## <a name="next-steps"></a>次の手順
- OLE DB ドライバーを使用して[Azure Active Directory に対する認証を](../features/using-azure-active-directory.md)行います。

- OLE DB ドライバーを使用して[認証資格情報をユーザーに要求](../help-topics/sql-server-login-dialog.md)します。