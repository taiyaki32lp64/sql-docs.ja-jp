---
title: パスワード ポリシー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- ALTER LOGIN statement
- passwords [SQL Server], policy enforcement
- logins [SQL Server], passwords
- CHECK_EXPIRATION option
- complex passwords [SQL Server]
- passwords [SQL Server], expiration
- manual bad password count resets
- MUST_CHANGE option
- expiration [SQL Server]
- expired password [SQL Server]
- symbols [SQL Server]
- NetValidatePasswordPolicy() API
- passwords [SQL Server]
- password policy [SQL Server]
- resetting bad password counts
- security [SQL Server], passwords
- CHECK_POLICY option
- passwords [SQL Server], symbols
- bad password counts
- passwords [SQL Server], complexity
- characters [SQL Server], password policies
ms.assetid: c0040c0a-a18f-45b9-9c40-0625685649b1
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7b28043d797585496686dea6fd0c5fad276f16b9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187967"
---
# <a name="password-policy"></a>パスワード ポリシー
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows のパスワード ポリシー メカニズムに対応しています。 パスワード ポリシーは [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用するログインに適用され、パスワードを持つ包含データベース ユーザーに適用されます。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]内部で使用されるパスワードに、Windows で使用されているものと同じ複雑性ポリシーおよび有効期限ポリシーを適用できます。 この機能は `NetValidatePasswordPolicy` API に依存します。  
  
## <a name="password-complexity"></a>パスワードの複雑性  
 パスワードの複雑性のポリシーは、使用可能なパスワードの数を増やすことにより、総当り攻撃を防ぐようにデザインされています。 パスワードの複雑性のポリシーが適用される場合、新しいパスワードは次のガイドラインを満たしている必要があります。  
  
-   パスワードはユーザー アカウント名を含まない。  
  
-   パスワードは 8 文字以上である。  
  
-   パスワードは次の 4 つのカテゴリのうちの 3 つのカテゴリの文字を含む。  
  
    -   ラテン文字の大文字 (A ～ Z)  
  
    -   ラテン文字の小文字 (a ～ z)  
  
    -   算用数字 (0 ～ 9)  
  
    -   感嘆符 (!)、ドル記号 ($)、番号記号 (#)、パーセント記号 (%) などの英数字以外の文字  
  
 パスワードには最大 128 文字まで使用できます。 パスワードはできるだけ長く、複雑にすることをお勧めします。  
  
## <a name="password-expiration"></a>パスワードの有効期限  
 パスワードの有効期限のポリシーは、パスワードの寿命を管理します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] によってパスワードの有効期限が適用されている場合、ユーザーは古いパスワードを変更するよう通知され、有効期限が切れたパスワードを持つアカウントは無効になります。  
  
## <a name="policy-enforcement"></a>ポリシーの適用  
 パスワード ポリシーの適用は、SQL Server ログインごとに個別に構成できます。 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql) を使用して、SQL Server ログインのパスワード ポリシー オプションを構成します。 パスワード ポリシーの適用を構成する際に、次の規則が当てはまります。  
  
-   CHECK_POLICY を ON に変更した場合、次の動作が行われます。  
  
    -   CHECK_EXPIRATION も、明示的に OFF に設定されない限り、ON に設定されます。  
  
    -   パスワードの履歴が、現在のパスワード ハッシュの値に初期化されます。  
  
    -   **[アカウント ロックアウトの期間]** 、 **[アカウント ロックアウトのしきい値]** 、および **[ロックアウト カウンターのリセット]** も有効になります。  
  
-   CHECK_POLICY を OFF に変更した場合、次の動作が行われます。  
  
    -   CHECK_EXPIRATION も OFF に設定されます。  
  
    -   パスワード履歴は消去されます。  
  
    -   `lockout_time` の値がリセットされます。  
  
 ポリシー オプションの組み合わせには、サポートされないものがあります。  
  
-   MUST_CHANGE が指定された場合、CHECK_EXPIRATION および CHECK_POLICY は ON に設定されなければなりません。 ON に設定しない場合、ステートメントは失敗します。  
  
-   CHECK_POLICY を OFF に設定した場合、CHECK_EXPIRATION を ON に設定することはできません。 このオプションの組み合わせで ALTER LOGIN ステートメントを実行すると、ステートメントは失敗します。  
  
 CHECK_POLICY = ON を設定すると、次のようなパスワードは作成できなくなります。  
  
-   NULL または空文字列  
  
-   コンピューター名またはログイン名と同じ文字列  
  
-   "password"、"admin"、"administrator"、"sa"、"sysadmin" のいずれかの文字列  
  
 セキュリティ ポリシーは、Windows で設定する場合も、ドメインから受け取る場合もあります。 コンピューターでパスワード ポリシーを表示するには、ローカル セキュリティ ポリシーの MMC スナップイン (**secpol.msc**) を使用します。  
  
## <a name="related-tasks"></a>Related Tasks  
 [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
 [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
 [CREATE USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)  
  
 [ALTER USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-user-transact-sql)  
  
 [ログインの作成](authentication-access/create-a-login.md)  
  
 [データベース ユーザーの作成](authentication-access/create-a-database-user.md)  
  
## <a name="related-content"></a>関連コンテンツ  
 [強力なパスワード](strong-passwords.md)  
  
  
