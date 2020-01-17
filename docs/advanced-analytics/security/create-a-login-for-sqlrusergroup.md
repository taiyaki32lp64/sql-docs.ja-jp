---
title: SQLRUserGroup のログインｎ作成
description: 暗黙の認証を使用したループ バック接続の場合は、SQLRUserGroup に対して SQL Server でログインを作成し、ID 変換が呼び出し元のユーザーへ返るようにするため、ワーカー アカウントがサーバーにログインできるようにします。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714960"
---
# <a name="create-a-login-for-sqlrusergroup"></a>SQLRUserGroup のログインｎ作成
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

スクリプト内の[ループ バック接続](../../advanced-analytics/concepts/security.md#implied-authentication)が*信頼関係接続*を指定するとき、[SQLRUserGroup](../concepts/security.md#sqlrusergroup) のための [SQL Server へのログイン](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login)を作成すると、あなたのコードを含むオブジェクトの実行に使用される ID は Windows のユーザー アカウントです。

信頼関係接続とは、接続文字列に `Trusted_Connection=True` を持つ接続のことです。 SQL Server が信頼関係接続を指定する要求を受信すると、現在の Windows ユーザーの ID にログインがあるかどうかを確認します。 ワーカー アカウント (**SQLRUserGroup** からの MSSQLSERVER01 など) として実行されている外部プロセスの場合、既定ではこれらのアカウントにはログインがないため、要求は失敗します。

**SQLServerRUserGroup** のログインを作成することによって、接続エラーを回避できます。 ID と外部プロセスの詳細については、「[機能拡張フレームワークのセキュリティの概要](../concepts/security.md)」を参照してください。

> [!Note]
> **SQLRUserGroup** に "ローカル ログオンを許可する" アクセス許可があることを確認します。 既定では、この権限はすべての新しいローカル ユーザーに与えられますが、グループ ポリシー付きの組織の一部では、この権限が無効になる場合があります。

## <a name="create-a-login"></a>ログインを作成します

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]のオブジェクト エクスプローラーで、 **[セキュリティ]** を展開し、 **[ログイン]** を右クリックして、 **[新しいログイン]** を選択します。

2. **[ログイン - 新規作成]** ダイアログ ボックスで、 **[検索]** をクリックします。 (まだボックスに何も入力しないでください)。
    
     ![[検索] をクリックして Machine Learning の新しいログインを追加する](media/implied-auth-login1.png "[検索] をクリックして Machine Learning の新しいログインを追加する")

3. **[ユーザーまたはグループの選択]** ボックスで、 **[オブジェクトの種類]** ボタンをクリックします。

     ![オブジェクトの種類を検索して Machine Learning の新しいログインを追加する](media/implied-auth-login2.png "オブジェクトの種類を検索して Machine Learning の新しいログインを追加する")

4. **[オブジェクトの種類]** ダイアログ ボックスで、 **[グループ]** を選択します。 他のチェック ボックスはすべてオフにします。

     ![[オブジェクトの種類] ダイアログ ボックスで [グループ] を選択する](media/implied-auth-login3.png "[オブジェクトの種類] ダイアログ ボックスで [グループ] を選択する")

4. **[詳細]** をクリックして、検索する場所が現在のコンピューターであることを確認し、 **[検索開始]** をクリックします。

     ![[検索開始] をクリックしてグループの一覧を取得する](media/implied-auth-login4.png "[検索開始] をクリックしてグループの一覧を取得する")

5. サーバー上のグループ アカウントの一覧を、`SQLRUserGroup` で始まるものが見つかるまでスクロールします。
    
    + Launchpad サービスの_既定のインスタンス_に関連付けられているグループの名前は、R または Python もしくはその両方のどれをインストールしたかにかかわらず、常に **SQLRUserGroup** です。 既定のインスタンスに対してのみ、このアカウントを選択します。
    + _名前付きインスタンス_を使用している場合、インスタンス名は、既定のワーカー グループ名である `SQLRUserGroup` に追加されます。 たとえば、インスタンスの名前が "MLTEST" の場合、このインスタンスの既定のユーザー グループ名は **SQLRUserGroupMLTest** となります。
 
    ![サーバー上のグループの例](media/implied-auth-login5.png "サーバー上のグループの例")
   
5. **[OK]** をクリックして [詳細設定] ダイアログ ボックスを閉じます。

    > [!IMPORTANT]
    > インスタンスに適切なアカウントを選択していることを確認してください。 各インスタンスは、独自の Launchpad サービスと、そのサービス用に作成されたグループのみを使用できます。 インスタンスは、Launchpad サービスまたはワーカー アカウントを共有できません。

6. **[OK]** をもう一度クリックして、 **[ユーザーまたはグループの選択]** ダイアログ ボックスを閉じます。

7. **[ログイン - 新規作成]** ダイアログ ボックスで、 **[OK]** をクリックします。 既定では、ログインは **Public** ロールに割り当てられ、データベース エンジンに接続するためのアクセス許可を与えられます。

## <a name="next-steps"></a>次の手順

+ [セキュリティの概要](../concepts/security.md)
+ [機能拡張フレームワーク](../concepts/extensibility-framework.md)
