---
title: ADO セキュリティ デザインの問題 |Microsoft Docs
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ADO, security
ms.assetid: 86b83a38-efdf-4831-a6d5-7e470d517d1c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f638f6e48dccccd91849f02c65331d9212f9bbb7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67927033"
---
# <a name="ado-security-design-features"></a>ADO セキュリティ デザイン機能
次のセクションでは、セキュリティ デザイン機能で ActiveX データ オブジェクト (ADO) 2.8 以降について説明します。 セキュリティを強化する ADO 2.8 行ったこれらの変更。 Windows Vista での Windows DAC 6.0 に含まれている、ADO 6.0 では、します機能的には、Windows XP および Windows Server 2003 で MDAC 2.8 に含まれていた ADO 2.8。 このトピックでは、ADO 2.8 以降ではアプリケーションの最適なセキュリティ保護する方法についての情報を提供します。

> [!IMPORTANT]
>  ADO の以前のバージョンからアプリケーションを更新する場合は、顧客に展開する前に、非実稼働コンピューターに更新されたアプリケーションをテストすることをお勧めします。 これにより、更新されたアプリケーションを展開する前に、互換性の問題を認識を確保できます。

## <a name="internet-explorer-file-access-scenarios"></a>インターネット エクスプ ローラーのファイル アクセスのシナリオ
 ADO 2.8 以降の動作方法を使用すると次の機能の効果は、Internet Explorer で Web ページをスクリプト化します。

### <a name="revised-and-improved-security-warning-message-box-now-used-to-alert-users"></a>改訂および強化されたセキュリティの警告メッセージ ボックスがユーザーに警告を使用するようになりました
 ADO 2.7 以降では、次の警告メッセージには、信頼されていないプロバイダーから ADO コードを実行する際にスクリプト化された Web ページが表示されます。

```console
This page accesses data on another domain. Do you want to allow this? To
avoid this message in Internet Explorer, you can add a secure Web site to
your Trusted Sites zone on the Security tab of the Internet Options dialog
box.
```

 ADO 2.8 以降の上記のメッセージに表示されなくなります。 代わりに、このコンテキストで、次のメッセージが表示されます。

```console
This Website uses a data provider that may be unsafe. If you trust the
Website, click OK, otherwise click Cancel.
```

 上記のメッセージで、ユーザーがいずれかの選択肢の影響を把握しながら、十分な情報に基づいて意思決定を行うことはできます。

-   ユーザーは、サイトを信頼する場合 [ok] をクリックするとにより、すべてのディスクの安全なコード (すべての ADO メソッドとプロパティが、このトピックの後半で説明されているディスクにアクセス可能な Api の例外) を実行し、ブラウザー ウィンドウでを実行します。

-   ユーザーが、サイトを信頼していない場合は、全体の実行からのデータ アクセス用の ADO コードをブロック [キャンセル] をクリックします。

### <a name="disk-accessible-code-limited-now-to-trusted-sites"></a>ディスクにアクセス可能なコードが信頼済みサイトに今すぐに制限されます。
 追加のデザインの変更を加えて ado 2.8 具体的には、限られた可能性から読み取りまたは書き込みをローカル コンピューター上のファイルを公開する可能性があります Api の機能を制限します。 さらにされている API のメソッドをここでは Internet Explorer を実行するときに、安全性に限定されています。

-   ADO の**Stream**オブジェクトの場合、 [LoadFromFile](../../ado/reference/ado-api/loadfromfile-method-ado.md)または[SaveToFile](../../ado/reference/ado-api/savetofile-method.md)メソッドを使用します。

-   ADO の**レコード セット**オブジェクトのいずれか、[保存](../../ado/reference/ado-api/save-method.md)メソッドまたは[オープン](../../ado/reference/ado-api/open-method-ado-recordset.md)場合などのメソッドか、 **adCmdFile**オプションを設定または[Microsoft OLE DB Persistence Provider (MSPersist)](../../ado/guide/appendixes/microsoft-ole-db-persistence-provider-ado-service-provider.md)使用されます。

 これらの制限の可能性のあるディスクにアクセス可能な関数のセットは、ADO 2.8 以降、Internet Explorer でこれらのメソッドを使用するコードが実行される場合の次の動作が発生します。

-   コードを提供するサイトは、信頼済みサイト ゾーンの一覧に以前追加された、コードは、ブラウザーで実行し、ローカル ファイルにアクセスを許可します。

-   サイトが信頼済みサイト ゾーンの一覧に表示されない場合は、コードはブロックされ、ローカル ファイルへのアクセスが拒否されました。

    > [!NOTE]
    >  Ado 2.8 以降、ユーザーすれば、警告を表示またはサイトを信頼済みサイト ゾーンの一覧に追加することをお勧めはできません。 そのため、信頼済みサイト リストの管理はデプロイまたはローカル ファイル システムへのアクセスを必要とする Web サイトに基づくアプリケーションをサポートしているユーザーの責任です。

### <a name="access-blocked-to-the-activecommand-property-on-recordset-objects"></a>ActiveCommand プロパティ レコード セット オブジェクトにブロックされるアクセス
 ADO 2.8 が今すぐへのアクセスをブロックして Internet explorer を実行するとき、 [ActiveCommand](../../ado/reference/ado-api/activecommand-property-ado.md)プロパティをアクティブな**Recordset**オブジェクトし、エラーが返されます。 信頼済みサイトのリストに登録されている Web サイトから、ページを取得するかどうかに関係なく、エラーが発生します。

### <a name="changes-in-handling-for-ole-db-providers-and-integrated-security"></a>OLE DB プロバイダーと統合セキュリティの処理の変更
 ADO 2.7 および潜在的なセキュリティの問題と懸念事項の以前のバージョンを確認する際は、次のシナリオが見つかりました。

 場合によっては、統合セキュリティをサポートしている OLE DB プロバイダーで[DBPROP_AUTH_INTEGRATED](https://msdn.microsoft.com/library/windows/desktop/ms712973.aspx)プロパティは、他のサーバーへの接続が意図せずに ADO 接続オブジェクトを再利用をスクリプト化された Web ページを許可できます可能性がありますユーザーの現在のログイン資格情報を使用します。 これを防ぐには、ADO 2.8 以降は、提供、または、統合セキュリティを提供しないが選択した方法に応じて、OLE DB プロバイダーを処理します。

 信頼済みサイト ゾーンの一覧に表示されているサイトから読み込まれた Web ページは、次の表は、ADO 2.8 以降が各ケースでの ADO 接続を管理する方法の詳細を提供します。

|IE 設定、ユーザー認証をログオンします。|"Integrated Security"および UID および PWD はプロバイダーのサポート (SQLOLEDB) を指定します。|プロバイダーでは、"Integrated Security"(JOLT、MSDASQL、MSPersist) をサポートしていません|プロバイダーは、"Integrated Security"をサポートし、SSPI (UID/PWD が指定されていない) に設定されています。|
|------------------------------------------------|----------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------|
|現在のユーザー名とパスワードで自動的にログオン|接続の許可|接続の許可|接続の許可|
|ユーザー名とパスワードを入力|接続の許可|接続が失敗します。|接続が失敗します。|
|イントラネット ゾーンでのみ自動ログオン|接続の許可|セキュリティの警告プロンプトを表示|セキュリティの警告プロンプトを表示|
|匿名ログオン|接続の許可|接続が失敗します。|接続が失敗します。|

 セキュリティの警告を今すぐが表示される場合は、メッセージ ボックスには、ユーザーが通知されます。

```console
This Website is using your identity to access a data source. If you trust this Website, click OK, otherwise click Cancel.
```

 上記のメッセージより十分な情報に基づいて意思決定を行い、続行できます。

> [!NOTE]
>  信頼されていないサイト (つまり、信頼済みサイト ゾーンの一覧に表示されないサイト) のプロバイダーも (このセクションで説明したように) として信頼されていない場合は、ユーザーが行、安全でないプロバイダーに関する警告、および 2 つ目の警告で 2 つのセキュリティ警告を表示可能性があります、自分の id を使用しようとしてください。 ユーザーは、最初の警告に [ok] をクリックすると、Internet Explorer の設定と、前の表で説明されている応答の動作のコードが実行されます。

## <a name="controlling-whether-password-text-is-returned-in-ado-connection-strings"></a>ADO 接続文字列にパスワードのテキストを返すかどうかを制御します。
 値を取得すると、 [ConnectionString](../../ado/reference/ado-api/connectionstring-property-ado.md)プロパティを ADO**接続**オブジェクトを次のイベントが発生します。

1.  接続が開いている場合、初期化し、呼び出しを基になる OLE DB プロバイダー接続文字列を取得します。

2.  OLE DB プロバイダーの設定に応じて、 [DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO](https://msdn.microsoft.com/library/windows/desktop/ms714905.aspx)プロパティ、パスワードは返されるその他の接続文字列情報と共に含まれています。

 たとえば場合、ADO 接続の動的プロパティ**Persist Security Info**に設定されている**True**、パスワード情報が返される接続文字列に含まれています。 それ以外の場合、基になるプロバイダーにプロパティを設定する場合**False** (たとえばで SQLOLEDB プロバイダー) ではパスワードの情報を省略すると、返される接続文字列にします。

 サード パーティ製を使用している場合 (つまり、Microsoft 以外) チェックする可能性があります、ADO アプリケーション コードと共に OLE DB プロバイダー、方法、 **DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO**を決定するプロパティが実装されているかどうかを含めることADO 接続文字列にパスワードの情報が許可されます。

## <a name="checking-for-non-file-devices-when-loading-and-saving-recordsets-or-streams"></a>非ファイル デバイスを読み込んで、レコード セットまたはストリームを保存するときのチェック
 ADO 2.7 およびそれ以前のファイル入出力操作など[オープン](../../ado/reference/ado-api/open-method-ado-recordset.md)と[保存](../../ado/reference/ado-api/save-method.md)で読み取りし、書き込みのファイル ベースのデータによってにより、URL またはファイル名を使用するディスク以外の指定に使用されました。ファイルの種類に基づいています。 たとえば、LPT1、COM2、PRN します。TXT、AUX のプリンターと補助デバイス間でシステムを使用して、特定の入力/出力の別名として使用できます。

 ADO 2.8 以降では、この機能が更新されました。 オープンと保存の**Recordset**と**Stream**オブジェクトの場合、ADO が今すぐ URL またはファイル名で指定された入力または出力のデバイスが実際のファイルであることを確認するファイルの種類のチェックを実行します。

> [!NOTE]
>  ファイルの型チェックこのセクションで説明したようにのみ適用されます Windows 2000 以降。 Windows 98 など、Windows の以前のリリースで ADO 2.8 以降が実行されている場合に適用されません。
