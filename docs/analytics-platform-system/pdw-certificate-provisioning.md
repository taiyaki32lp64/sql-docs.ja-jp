---
title: PDW 証明書のプロビジョニング - Analytics Platform System |Microsoft Docs
description: PDW の証明書の準備 ページの Analytics Platform System Configuration Manager では、インポートまたは PDW リージョンで使用される証明書を削除します。
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: af6d4df964820ced9f4d79b67859e010a895bc29
ms.sourcegitcommit: 99847f34e949a5c3c58565d76be3abf5b80f9632
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/05/2019
ms.locfileid: "55742122"
---
# <a name="pdw-certificate-provisioning---analytics-platform-system"></a>PDW 証明書のプロビジョニング - Analytics Platform System
**PDW 証明書のプロビジョニング**Analytics Platform System のページ**Configuration Manager**をインポートまたは PDW リージョンで使用される証明書を削除します。 使用して、接続の暗号化に証明書は、SQL Server PDW のドライバーを使用するツールの SQL Server クライアント経由で、コントロール ノードにセキュリティで保護された通信を支援できます、 [Admin Console](monitor-the-appliance-by-using-the-admin-console.md)、Integration Services で読み込まれるとします。  
  
## <a name="prerequisites"></a>前提条件  
証明書をインストールする前に、次の手順を実行します。  
  
1.  セキュリティで保護された証明書を取得します。 セキュリティで保護された証明書を取得する方法については、必要がある場合は、Microsoft サポートにお問い合わせください。  
  
2.  証明書をパスワードで保護された PFX ファイル内の管理ノードに保存します。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>セキュリティ上の理由から、信頼された証明書を取得します  
SQL Server PDW は、コントロールのノードへの接続の暗号化に証明書の使用をサポートしています接続など、 **Admin Console**します。  
  
既定で、 **Admin Console**プライバシーがないサーバーの認証を提供する自己署名証明書が含まれています。 これは、ままにできます通信で中間者攻撃に対して脆弱になります。 ユーザーは、自己署名証明書を使用して、管理コンソールに接続するとき、Internet Explorer には、エラーが返されます。「この web サイトのセキュリティ証明書に問題があるです」  
  
自己署名証明書を使って接続が、クライアントとサーバー間のインフライトのデータを暗号化しますが、接続は、攻撃者から危険にさらされてもです。  
  
> [!WARNING]  
> アプライアンス管理者は、セキュリティで保護された接続があり、Internet Explorer でレポートされるエラーを削除するには、クライアントによって認識される信頼された証明機関にチェーンされている証明書をすぐに取得する必要があります。  
  
証明書のパスは、コントロールのノード (推奨) クラスターの IP アドレスにマップされる完全修飾ドメイン名またはユーザーにアクセスする、ブラウザーのアドレス バーに入力する名前を含める必要があります、 **Admin Console**します。  
  
Analytics Platform System を使用して、**Configuration Manager**を追加または信頼された証明書を削除します。 Microsoft Windows HTTP サービス証明書の構成ツールを使用して直接 (**winHttpCertCfg.exe**)、証明書の管理にはサポートされていません。  
  
## <a name="import-or-remove-the-certificate"></a>インポートまたは証明書を削除  
次の手順では、インポートまたはアプライアンスの証明書を削除する方法を示しています。

> [!WARNING]
> 有効期限が切れた証明書を書き換えるには、新しいものをインポートする前に既存の証明書を削除する必要があります。
  
### <a name="to-import-the-certificate"></a>証明書をインポートするには  
  
1.  起動、 **Configuration Manager**します。 詳細については、次を参照してください。 [Configuration Manager の起動&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)します。  
  
2.  左側のウィンドウで、 **Configuration Manager**、展開**並列データ ウェアハウスのトポロジ**、 をクリックし、**証明書**します。  
  
3.  選択**証明書をインポートし、それを使用するアプライアンスを構成**、 をクリックし、**参照**を参照し、証明書ファイルを選択します。  
  
4.  証明書のパスワードを入力、**パスワード**フィールド。  
  
5.  クリックして**適用**アプライアンス用の証明書を構成します。  
  
SQL Server PDW では、インポートした証明書を使用して現在の接続は暗号化されませんが、新しい接続の証明書を使用します。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>以前にインポートした証明書を削除するには  
  
1.  起動、 **Configuration Manager**します。 詳細については、次を参照してください。 [Configuration Manager の起動&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)します。  
  
2.  左側のウィンドウで、 **Configuration Manager**、展開**並列データ ウェアハウスのトポロジ**、 をクリックし、**証明書**します。  
  
3.  選択**アプライアンスでプロビジョニングされたすべての証明書を削除**します。  
  
4.  クリックして**適用**アプライアンスから以前にインポートした証明書を削除します。  
  
SQL Server PDW では、現在の接続の暗号化に続行されますが、新しい接続には、削除した証明書は使用されません。  
  
![DWConfig アプライアンス PDW の証明書](./media/pdw-certificate-provisioning/SQL_Server_PDW_DWConfig_ApplPDWCert.png "SQL_Server_PDW_DWConfig_ApplPDWCert")  
  
## <a name="see-also"></a>参照  
[Configuration Manager の起動&#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
<!-- MISSING LINKS [HDInsight Certificate Provisioning &#40;Analytics Platform System&#41;](hdinsight-certificate-provisioning.md)  -->  
  
