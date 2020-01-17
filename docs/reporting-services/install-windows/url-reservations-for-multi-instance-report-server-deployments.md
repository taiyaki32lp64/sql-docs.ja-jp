---
title: レポート サーバーの複数インスタンス配置における URL 予約 | Microsoft Docs
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
ms.assetid: f67c83c0-1f74-42bb-bfc1-e50c38152d3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0a09d7c391af0d8800f5d9c66d40ab7ba0c2cbf4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62513284"
---
# <a name="url-reservations-for-multi-instance-report-server-deployments"></a>レポート サーバーの複数インスタンス配置における URL 予約
  同じコンピューターに [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の複数のインスタンスをインストールする場合は、インスタンスごとに URL 予約を定義する方法を検討する必要があります。 各インスタンス内のレポート サーバー Web サービスと [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] には、それぞれ 1 つ以上の URL 予約が必要です。 予約はすべて、HTTP.SYS 内で一意にする必要があります。  
  
 重複する URL があれば、サービスの起動時に行われる URL の登録の際に検出されます。 一意でない URL 予約を作成した場合、サービスを起動するまで名前の競合が検出されない可能性があります。 このため、名前付け規則に従ってすべての値が一意になるようにしてください。  
  
## <a name="default-naming-conventions"></a>既定の名前付け規則  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の名前付きインスタンス内にインストールできます。 名前付きインスタンス内にレポート サーバーをインストールまたは構成すると、 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] に用意されている既定の URL 予約の仮想ディレクトリにインスタンス名が自動的に含められます。 次の表に、既定のインスタンスと名前付きインスタンスの URL 予約を示します。  
  
|SQL Server インスタンス|既定の URL 予約|  
|-------------------------|-----------------------------|  
|既定 (MSSQLServer)|`https://+:80/reportserver`|  
|名前付き (MynamedInstance)|`https://+:80/reportserver_MyNamedInstance`|  
  
 名前付きインスタンスの場合は、仮想ディレクトリにインスタンス名が含まれます。 既定のインスタンスと名前付きインスタンスは同じポートでリッスンしますが、一意の仮想ディレクトリ名によって、どちらのレポート サーバーが要求を受け取るかが決定されます。  
  
 レポート サーバー インスタンスは、仮想ディレクトリ名を使用して区別することをお勧めします。 仮想ディレクトリ名によって URL と対象インスタンスの対応関係が明確になり、アプリケーション名がシステム全体で一意になります。  
  
## <a name="custom-naming-conventions"></a>カスタム名前付け規則  
 インスタンス名を使用することをお勧めしますが、URL 構文と独自の名前付け規則を使用して URL 予約の一意の名前の制約を満たすこともできます。 次の例はそれぞれ、インスタンスごとに一意の URL を作成するための方法を示しています。  
  
|既定のレポート サーバー インスタンス (MSSQLSERVER)|ReportServer_MyNamedInstance|一意性|  
|----------------------------------------------------|-----------------------------------|----------------|  
|`https://+:80/reportserver`|`https://+:8888/reportserver`|各インスタンスが、別々のポートでリッスンします。|  
|`https://www.contoso.com/reportserver`|`https://SRVR-46/reportserver`|各インスタンスが、別々のサーバー名 (完全修飾ドメイン名およびコンピューター名) に応答します。|  
  
## <a name="uniqueness-requirements"></a>一意性の要件  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] の基になるテクノロジには、一意の名前に関する要件があります。 HTTP.SYS のリポジトリ内の URL はすべて一意にする必要があります。 URL は、ポート、ホスト名、または仮想ディレクトリ名を変えることで一意にできます。 [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] では、同一プロセス内の各アプリケーション ID が一意である必要があります。 この要件は、仮想ディレクトリ名に影響します。 この要件では、同一レポート サーバー インスタンス内では重複する仮想ディレクトリ名を使用できないことが規定されています。  
  
## <a name="see-also"></a>参照  
 [レポート サーバー URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)   
 [URL の構成 &#40;SSRS 構成マネージャー&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md)  
  
  
