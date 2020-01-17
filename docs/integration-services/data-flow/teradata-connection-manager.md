---
title: Teradata 接続マネージャーの使用 | Microsoft Docs
ms.custom: ''
ms.date: 11/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d520f83f515694bd8852ce11ea13fce7f3213596
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245122"
---
# <a name="use-the-teradata-connection-manager"></a>Teradata 接続マネージャーの使用

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Teradata 接続マネージャーを使用すると、パッケージを有効にして、Teradata データベースからデータを抽出したり、Teradata データベースにデータを読み込んだりすることができます。

Teradata 接続マネージャーの `ConnectionManagerType` プロパティを *TERADATA* に設定します。

## <a name="configure-the-teradata-connection-manager"></a>Teradata 接続マネージャーの構成

接続マネージャーの構成の変更は、実行時に Integration Services によって解決されます。 Teradata データソースへの接続を追加するには、 **[Teradata 接続マネージャー エディター]** ウィンドウに情報を入力します。

![[Teradata 接続マネージャーエディター] ウィンドウ](media/teradata-connection-manager.png)

1. **[名前]** ボックスに、接続の名前を入力します。 既定の名前は、 **[Teradata 接続マネージャー]** です。

1. (省略可能) **[説明]** ボックスに、接続の説明を入力します。

1. **[サーバー名]** ボックスに、接続先の Teradata サーバーの名前を入力します。

1. **[認証]** で、次のいずれかの操作を行います。

   - Windows 認証を使用するには、 **[Windows 認証を使用する]** を選択します。
   - Teradata データベース認証を使用するには、 **[Teradata 認証を使用する]** を選択し、この種類の認証に対して次の資格情報を入力します。
     - **[メカニズム]** ボックスに、使用するセキュリティ チェック メカニズムを入力します。 有効なメカニズム値には、TD1、TD2、LDAP、KRB5、KRB5C、NTLM、NTLMC があります。
     - **[パラメーター]** ボックスに、入力したセキュリティ チェック メカニズムに必要なパラメーターの種類を入力します。
     - **[ユーザー名]** ボックスに、Teradata データベースへの接続に使用するユーザー名を入力します。  
     - **[パスワード]** ボックスに、ユーザーの Teradata データベースのパスワードを入力します。

1. (省略可能) **[既定のデータベース]** ドロップダウン リストで、接続先の Teradata データベースを選択します。 このデータベースアクセスの権限が不正である場合は、エラーが表示されます。その後、データベース名を手動で入力できます。

1. (省略可能) **[アカウント]** ボックスに、ユーザー名に対応するアカウントの名前を入力します。 この値が空の場合は、データベースの直接の所有者のアカウントが使用されます。
1. **[OK]** を選択します。

## <a name="custom-property"></a>カスタム プロパティ

カスタムプロパティ `UseUTF8CharSet` では、UTF-8 文字セットを使用するかどうかを指定します。 既定値は *True*です。

プロパティを設定するには、次の操作を行います。

1. SQL Server Data Tools (SSDT) を開きます。
1. **[接続マネージャー]** 領域で、 **[Teradata 接続マネージャー]** を右クリックし、 **[プロパティ]** を選択します。
1. **[プロパティ]** ウィンドウで、`UseUTF8CharSet` プロパティについて *[True]* または *[False]* を選択します。

## <a name="troubleshoot-the-teradata-connection-manager"></a>Teradata 接続マネージャーのトラブルシューティング

Teradata Open Database Connectivity (ODBC) ドライバーへの Teradata 接続マネージャー呼び出しをログに記録するには、[ODBC データ ソースの管理者] で Windows ODBC トレースを有効にします。

## <a name="next-steps"></a>次のステップ

- [Teradata ソース](teradata-source.md)を構成する。
- [Teradata 変換先](teradata-destination.md)を構成する。
- ご質問がある場合は、[技術者コミュニティ](https://aka.ms/AA5u35j)を参照してください。
