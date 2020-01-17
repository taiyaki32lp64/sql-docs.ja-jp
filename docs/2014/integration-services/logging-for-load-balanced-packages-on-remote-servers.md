---
title: リモート サーバー上でパッケージが分散負荷のログ記録 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], remote packages
ms.assetid: fd571567-b625-4f9a-8b7e-42c5c588b11b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 64dec3a89b883d6b3234f65896bb89d3bfde5305
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057853"
---
# <a name="logging-for-load-balanced-packages-on-remote-servers"></a>リモート サーバー上の負荷分散パッケージのログ記録
  すべての子パッケージで同じログ プロバイダーを使用し、これらの出力先を同じにすれば、さまざまなサーバーで実行されているすべての子パッケージに関するログの管理が容易になります。 すべての子パッケージに共通するログ ファイルを作成する方法の 1 つとして、イベントのログが SQL Server ログ プロバイダーに記録されるように子パッケージを構成することができます。 すべてのパッケージが、同じデータベース、同じサーバー、同じサーバー インスタンスを使用するように構成できます。  
  
 管理者は、1 台のサーバーにログオンするだけで、すべての子パッケージに関するログ ファイルを確認できます。  
  
## <a name="related-tasks"></a>Related Tasks  
 パッケージでログ記録を有効にする方法については、「 [SQL Server Data Tools でパッケージのログ記録を有効にする](../../2014/integration-services/enable-package-logging-in-sql-server-data-tools.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)  
  
  
