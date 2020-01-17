---
title: 証明書のプロビジョニング
description: Analytics Platform System での証明書のプロビジョニング。
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 669e65a7d27b208d861a33618d889707134dfefa
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2019
ms.locfileid: "74400513"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Analytics Platform System での証明書のプロビジョニング
Analytics Platform System**Configuration Manager**の**pdw 証明書のプロビジョニング**ページでは、pdw によって使用される証明書をインポートまたは削除します。 

を使用すると、証明書を使用して接続を暗号化することで、SQL Server クライアント、SQL Server PDW ドライバーを使用するツール、[管理コンソール](monitor-the-appliance-by-using-the-admin-console.md)、および Integration Services を使用して、制御ノードとの通信をセキュリティで保護することができます。 
  
## <a name="prerequisites"></a>前提条件  
証明書をインストールする前に、次の手順を実行します。  
  
1.  セキュリティで保護された証明書を取得します。 セキュリティで保護された証明書を取得する方法の詳細については、Microsoft サポートにお問い合わせください。  
  
2.  パスワードで保護された PFX ファイルのコントロールノードに証明書を保存します。  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>セキュリティ上の理由から、信頼された証明書を取得する  
SQL Server PDW は、証明書を使用してコントロールノードへの接続を暗号化することをサポートしています。**管理コンソール**への接続が含まれます。  
  
既定では、**管理コンソール**には、サーバー認証ではなく、プライバシーを提供する自己署名証明書が含まれています。 これにより、中間者攻撃に対して通信が脆弱になる可能性があります。 ユーザーが自己署名証明書を使用して管理コンソールに接続すると、Internet Explorer は "この web サイトのセキュリティ証明書に問題があります" というエラーを返します。  
  
自己署名証明書を使用した接続では、クライアントとサーバーの間のデータが暗号化されますが、接続は攻撃者の危険にさらされます。  
  
> [!WARNING]  
> アプライアンス管理者は、セキュリティで保護された接続を確立し、Internet Explorer が報告するエラーを削除するために、クライアントによって認識される信頼された証明機関にチェーンする証明書をすぐに取得する必要があります。  
  
証明書のパスには、管理**コンソール**にアクセスするためにユーザーがブラウザーのアドレスバーに入力する、制御ノードのクラスター IP アドレス (推奨) または名前にマップされる完全修飾ドメイン名が含まれている必要があります。  
  
Analytics Platform System**Configuration Manager**を使用して、信頼された証明書を追加または削除します。 Microsoft Windows HTTP サービス証明書構成ツール (**winhttpcertcfg.exe**) を直接使用して証明書を管理することはサポートされていません。  
  
## <a name="import-or-remove-the-certificate"></a>証明書をインポートまたは削除する  
次の手順は、アプライアンス証明書をインポートまたは削除する方法を示しています。  
  
### <a name="to-import-the-certificate"></a>証明書をインポートするには  
  
1.  **Configuration Manager**を起動します。  
詳細については、「 [Configuration Manager &#40;Analytics Platform System&#41;の起動](launch-the-configuration-manager.md)」を参照してください。  

2.  **Configuration Manager**の左ペインで、[**並列データウェアハウストポロジ**] を展開し、[**証明書**] をクリックします。  
  
3.  [**証明書のインポート] を選択し、それを使用するようにアプライアンスを構成**します。次に、[**参照**] をクリックして、証明書ファイルを参照して選択します。  
  
4.  [**パスワード**] フィールドに証明書のパスワードを入力します。  
  
5.  [**適用**] をクリックして、アプライアンスの証明書を構成します。  
  
SQL Server PDW は、インポートされた証明書を使用して現在の接続を暗号化しませんが、新しい接続には証明書を使用します。  
  
### <a name="to-remove-the-previously-imported-certificate"></a>以前にインポートした証明書を削除するには  
  
1.  **Configuration Manager**を起動します。 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  **Configuration Manager**の左ペインで、[**並列データウェアハウストポロジ**] を展開し、[**証明書**] をクリックします。  
  
3.  [**アプライアンスでプロビジョニングされた証明書を削除する**] を選択します。  
  
4.  [**適用**] をクリックして、以前にインポートした証明書をアプライアンスから削除します。  
  
SQL Server PDW は引き続き現在の接続を暗号化しますが、新しい接続では削除された証明書を使用しません。  
  
![DWConfig アプライアンス PDW の証明書](media/dwconfig-appl-pdw-cert.png "DWConfig アプライアンス PDW 証明書")  
  
## <a name="see-also"></a>参照  
[Configuration Manager &#40;Analytics Platform System&#41;を起動します。](launch-the-configuration-manager.md)  
