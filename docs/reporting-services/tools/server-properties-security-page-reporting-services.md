---
title: '[サーバーのプロパティ] ([セキュリティ] ページ) - Reporting Services | Microsoft Docs'
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.serverproperties.security.f1
ms.assetid: f49aedc6-f145-4df1-8f69-d5d910f492c6
author: maggiesMSFT
ms.author: maggies
ms.date: 06/10/2016
ms.openlocfilehash: 0e29dcf7681d105f92b3bf187c38ebe764d2449e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571314"
---
# <a name="server-properties-security-page---reporting-services"></a>[サーバーのプロパティ]\([セキュリティ] ページ) - Reporting Services

  [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] の [!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] ページを使用すると、レポート サーバーを危険にさらす可能性のある機能を無効にできます。 これらの機能を無効にすることで一部の機能が制限されますが、特定の脅威を緩和することで、レポート サーバーのセキュリティ全体を向上させることができます。  
  
 このページを開くには:
 1) [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]を起動します。
 2) レポート サーバー インスタンスに接続します。
 3) レポート サーバー名を右クリックして、 **[プロパティ]** をクリックします。
 4) **[セキュリティ]** をクリックすると、このページが開きます。  
  
## <a name="options"></a>オプション

### <a name="enable-windows-integrated-security-for-report-data-sources"></a>[レポート データ ソースで Windows 統合セキュリティを有効にする]

 レポートを要求したユーザーの Windows セキュリティ トークンを使用してレポート データ ソースに接続するかどうかを指定します。  
  
 機能を無効にすると、レポート データ ソースのプロパティ ページにある Windows 統合セキュリティ機能が使用できなくなります。 ご利用のレポート データ ソースが Windows 統合セキュリティ用に構成されている場合、後でこの機能を無効にすると、レポート サーバーによってすべてのデータ ソース接続プロパティが即時に更新され、資格情報が要求されます。  
  
### <a name="enable-ad-hoc-reporting"></a>[カスタム レポートを有効にする]

 ユーザーがレポート ビルダーのレポートからアドホック クエリを実行できるようにするかどうかを指定します。実行できるようにした場合は、ユーザーが対象データをクリックすると新しいレポートが自動的に生成されます。  
  
 このオプションの設定によって、レポート サーバー上の **EnableLoadReportDefinition** プロパティの設定が **True** になるか **False**になるかが決まります。 このオプションをオフにすると、プロパティが **False** に設定され、レポート サーバーでデータ探索中に作成されるクリックスルー レポートが生成されません。 **LoadReportDefinition** メソッドへの呼び出しはすべてブロックされます。  
  
 この機能を無効にすることで、悪意のあるユーザーが **LoadReportDefinition** 要求でレポート サーバーを過負荷にするサービス拒否攻撃の脅威を緩和することができます。  
  
## <a name="see-also"></a>参照

 [レポート サーバーのプロパティを設定する&#40;Management Studio&#41;](../../reporting-services/tools/set-report-server-properties-management-studio.md) [Management Studio でレポート サーバーに接続する](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md) [レポート データ ソースに関する資格情報と接続情報を指定する](../../reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources.md) [Management Studio のレポート サーバーの F1 ヘルプ](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)
