---
title: 多言語配置とグローバル配置 (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c3d485f8-867c-4aa2-a90d-f38fda192534
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d53ff45452f90c5cf29f376ba01a395d2bbccf65
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "65482963"
---
# <a name="multi-lingual-and-global-deployments-master-data-services"></a>多言語配置とグローバル配置 (Master Data Services)
  [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]でサポートされているすべての言語によるコンポーネントとツールの配置がサポートされています。 詳細については、「 [SQL Server のローカル言語版](../../sql-server/install/local-language-versions-in-sql-server.md)」を参照してください。  
  
## <a name="how-languages-are-used"></a>言語の使用方法  
 次の表では、 [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] のコンポーネントとツールの言語サポートについて説明します。  
  
|コンポーネントまたはツール|説明|  
|-----------------------|-----------------|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] セットアップ|セットアップの言語とは異なる言語で [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションを使用できるようにし、サポートされるようにする場合は、英語版のセットアップ プログラムを選択します。 詳細については、下記の [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] の説明を参照してください。|  
|[!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)]|セットアップの言語によって、 [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] の言語が決まります。 たとえば、セットアップの言語としてドイツ語を選択した場合、そのコンピューターでは [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)] をドイツ語で使用できます。|  
|[!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)]|セットアップを英語で実行した場合、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] Web アプリケーションは、すべてのアプリケーション言語で使用でき、サポートされます。 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] は、これらのどのアプリケーション言語でも表示でき、クライアントの Web ブラウザーの言語設定に基づくロケール固有の入力を受け入れます。 言語設定が、サポートされないアプリケーション言語用に構成されている場合、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] は既定で英語に設定されます。<br /><br /> 英語以外の言語でセットアップを実行した場合、他のすべてのアプリケーション言語のリソースが含まれますが、クライアントでは、選択されたセットアップ言語以外の言語で [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] を使用することはできません。 セットアップの言語とは異なる言語で [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] にアクセスしようとすると、アプリケーションでデータ表示およびデータ入力に関する問題が発生することがあります。|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース (database)|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] データベース内の情報は、ロケール固有のものではありません。 そのため、 [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] は、日付や数値などの情報の表示方法を、クライアントの Web ブラウザーの言語設定によって決められた形式で決定することができます。|  
  
## <a name="see-also"></a>参照  
 [マスター データ サービスのインストール](install-master-data-services.md)  
  
  
