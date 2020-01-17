---
title: パスワード リセット
description: '[パスワードのリセット] ページでは、Analytics Platform System によって使用される管理者アカウントのパスワードを変更できます。'
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 952dbda04b4f7132406e3a6de4479afea1be92e7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400900"
---
# <a name="password-reset---analytics-platform-system"></a>パスワードリセット-分析プラットフォームシステム
[**パスワードのリセット**] ページでは、Analytics Platform System によって使用される管理者アカウントのパスワードを変更できます。  
  
> [!WARNING]  
> アプライアンスドメイン管理者のパスワードを更新するには、常に**Configuration Manager**を使用します。 その他の方法では、Analytics Platform System のすべてのコンポーネントを更新することができず、アプライアンスのアクセスに問題が発生する可能性があります。  
  
アプライアンスが配信されるときに、Analytics プラットフォームのシステムパスワードが付与されます。 アプライアンスを使用する場合は常に、パスワードを新しい値に変更してください。 更新するパスワードは3つあります。 パスワードは、互いに同じである必要はありません。  
  
**F<*xxxx*> \administrator**  
アプライアンスドメインの**管理者**。  
  
**.\Administrator**  
仮想マシンをホストするコンピューターのローカル**管理者**アカウント。  
  
> [!IMPORTANT]  
> アプライアンスの更新プログラム1では、 **Configuration Manager**は PDW VM のローカル管理者アカウントのパスワードを正しく変更しません。 これが必要な場合は、追加の手順について CSS にお問い合わせください。  
  
**sa**  
SQL Server の**sa**ログイン。 **sa**は、 **sysadmin**固定サーバーロールのメンバーであり、SQL Server 管理者です。 **Sa**ログインのパスワードは、 **ALTER login**ステートメントを使用して変更することもできます。  
  
## <a name="password-requirements"></a>パスワードの要件  
ドメイン管理者の資格情報とシステム管理者の資格情報の両方が、資格情報の種類ごとにパスワード強度ポリシーに従います。 ドメイン管理者の資格情報を変更すると、新しいパスワードが SQL Server PDW 全体で必要なドメインに更新されます。  
  
> [!IMPORTANT]  
> SQL Server PDW では、ドメイン管理者または**$** ローカル管理者のパスワードのドル記号 () はサポートされていません。 パスワードには **^% &** 文字を使用できますが、PowerShell ではこれらは特殊文字として扱われます。 これらの文字のいずれかがシステム管理者または SQL Server**sa**アカウントのパスワード (セットアップ時に**Adminpassword**および**PdwSAPassword**パラメーター) で使用されている場合、インストール、アップグレード、置換機能、修正プログラムなどのセットアップは失敗します。 現在のパスワードにサポートされていない文字が含まれている場合にアップグレードを成功させるには、アップグレードを実行する前に、これらの文字が含まれないようにパスワードを変更します。 アップグレードが完了したら、これらのパスワードを元の値に戻すことができます。 パスワードの要件の詳細については、「 [ALTER LOGIN](../t-sql/statements/alter-login-transact-sql.md)」を参照してください。  
  
## <a name="to-reset-a-password"></a>パスワードをリセットするには  
  
1.  コントロールノードに接続し、 **Configuration Manager** (**dwconfig .exe**) を起動します。 詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動](launch-the-configuration-manager.md)」を参照してください。  
  
2.  **Configuration Manager**の左側のウィンドウで、[**パスワードのリセット**] をクリックします。  
  
3.  [**アカウント**] ドロップダウンメニューから管理者の種類を選択し、[**パスワード**] ボックスと [**パスワードの確認**入力] ボックスに新しいパスワードを入力します。 [**適用**] をクリックして変更を保存します。  
  
    これらのアカウントに対して行った変更は、現在アクティブなセッションには影響しませんが、各ユーザーに対して次回ログオンを試行するときに適用されます。  
  
    ![SQL Server DWConfig パスワード](./media/password-reset/SQL_Server_PDW_DWConfig_TopPW.png "SQL_Server_PDW_DWConfig_TopPW")  
  
## <a name="see-also"></a>参照  
[ディレクトリサービス復元モードで AD ノードにログオンするための管理者パスワードを設定し &#40;DSRM&#41; &#40;Analytics Platform System&#41;](set-admin-password-for-logging-on-to-ad-nodes-in-directory-services-restore-mode.md)  
[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)  
  
