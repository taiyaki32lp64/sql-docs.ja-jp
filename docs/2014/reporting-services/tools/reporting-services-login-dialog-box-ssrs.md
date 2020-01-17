---
title: '[Reporting Services ログイン] ダイアログ ボックス (SSRS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.reportservicelogin.f1
ms.assetid: 2037d797-0b61-44c7-931f-6c689c3fc733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 232ee51614a668b07263c3e3a4182f23652135bf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099869"
---
# <a name="reporting-services-login-dialog-box-ssrs"></a>[Reporting Services ログイン] ダイアログ ボックス (SSRS)
  **[Reporting Services ログイン]** ダイアログ ボックスを使用すると、レポートをレポート サーバーにパブリッシュする際に使用する資格情報を指定できます。  
  
-   **注**展開のプロパティを設定するが初めてセット以降、レポート サーバーにレポートを発行した場合**TargetServerURL**プロジェクトでは、指定したサーバー名がのようなことを確認します`http://localhost/reportserver`、および not`http://localhost/reports`します。 ローカル サーバーの `reports` ディレクトリではなく `reportserver` ディレクトリを指定すると、このダイアログ ボックスが間接的に開かれます。 **TargetServerURL** の設定の詳細については、「[配置プロパティを設定する &#40;Reporting Services&#41;](set-deployment-properties-reporting-services.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Server**  
 レポート サーバーの名前を表示します。 たとえば、 `http://localhost/reportserver`のようにします。 既定のポート 80 と異なるポートを使用するレポート サーバーの場合は、ポート番号を含めます。 たとえば、`http://localhost:81/reportserver` のようにします。  
  
 **ユーザー名**  
 Web サービスへのログインに使用するユーザー名を入力します。  
  
 **Password**  
 Web サービスへのログインに使用するパスワードを入力します。  
  
## <a name="see-also"></a>関連項目  
 [データ接続、データ ソース、および Reporting Services の接続文字列](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [資格情報とレポート データ ソースに関する接続情報を指定](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)[レポート デザイナーの F1 ヘルプ](report-designer-f1-help.md)  
  
  
