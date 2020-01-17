---
title: rsAccessedDenied - Reporting Services エラー | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsAccessDenied error
ms.assetid: 2f76b1bf-96a2-4755-b76b-84e933220efc
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bfaad65431cc71c8fa7a6ec5ba24e13fa7692e99
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66099232"
---
# <a name="rsaccesseddenied---reporting-services-error"></a>rsAccessedDenied - Reporting Services エラー
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] エラー **rsAccessedDenied** は、操作を実行する権限がユーザーに与えられていない場合に発生します。 たとえば、レポートを開くためのロールが割り当てられていない場合や、必要な権限を使用してブラウザーを開かなかった場合などです。  
  
||  
|-|  
|**[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ネイティブ モード &#124; SharePoint モード|  
  
-   URL を指定してレポート サーバーへ直接アクセスしているときにこのエラーが発生した場合は、HTTP 401 エラーに例外がマップされます。  
  
-   レポート マネージャーやその他のツールを使用しているときに発生した場合は、エラー ページに表示されます。  
  
-   スケジュール設定された操作、サブスクリプション、または配信中に発生した場合は、レポート サーバーのログ ファイルにのみ記録されます。  
  
## <a name="details"></a>詳細  
  
|||  
|-|-|  
|**製品名**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|**イベント ID**|rsAccessedDenied|  
|**イベント ソース**|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|**コンポーネント**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|**メッセージ テキスト**|ユーザー 'mydomain\myAccount' には、この操作を行うのに必要な権限が与えられていません。 (rsAccessDenied) (ReportingServicesLibrary)。|  
  
## <a name="user-action"></a>ユーザーの操作  
 レポート サーバーのコンテンツや操作にアクセスする権限は、ロールの割り当てによって与えられます。 新規インストールを実行した時点では、ローカル管理者のみがレポート サーバーにアクセスできます。 他のユーザーがレポート サーバーにアクセスできるようにするには、ローカル管理者が、ドメインのユーザー アカウントやグループ アカウントを指定するロールの割り当て、ユーザーが実行できるタスクを定義する 1 つ以上のロール、およびスコープ (通常は、レポート サーバー フォルダー階層のルート ノードである [ホーム] フォルダー) を作成する必要があります。 レポート マネージャーを使用すると、ロールの割り当てを作成できます。 詳細については、SQL Server オンライン ブックの「ロールの割り当て」を参照してください。  
  
 このエラーは、レポート サーバーのローカル管理が原因で発生することもあります。 詳細については、「 [ローカル管理用のネイティブ モードのレポート サーバー &#40;SSRS&#41; の構成](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md)。  
  
## <a name="see-also"></a>関連項目  
 [ロールの割り当て](../security/role-assignments.md)   
 [ネイティブ モードのレポート サーバーに対する権限の許可](../security/granting-permissions-on-a-native-mode-report-server.md)   
 [ロールと権限 (Reporting Services)](../security/roles-and-permissions-reporting-services.md)  
  
  
