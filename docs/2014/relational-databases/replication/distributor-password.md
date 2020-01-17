---
title: ディストリビューター パスワード | Microsoft Docs
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configuredistributionwizard.distributorpassword.f1
ms.assetid: 52787c5e-c9ef-440e-a000-0787111b7dbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a6d3c7971f6d5e117ae923ee8697a4ec51e1a34e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721472"
---
# <a name="distributor-password"></a>[ディストリビューター パスワード]
  このサーバーをリモート ディストリビューターとして使用する 1 つ以上のパブリッシャーを、このウィザードの **[パブリッシャー]** ページで有効にしている場合は、レプリケーションが **distributor_admin** ログインを使用してパブリッシャーとリモート ディストリビューターとの間で確立する接続のパスワードを指定する必要があります。 このリモート ディストリビューターを使用するそれぞれのパブリッシャーに対して、パブリケーションの新規作成ウィザードまたはディストリビューションの構成ウィザードの **[管理パスワード]** ページに、同じパスワードを入力する必要があります。 ディストリビューターのセキュリティの詳細については、「[ディストリビューターのセキュリティ保護](security/secure-the-distributor.md)」を参照してください。  
  
## <a name="options"></a>および  
 **Password**  
 パブリッシャーとリモート ディストリビューターとの間の接続に使用する複雑なパスワードを入力します。  
  
 **[パスワードの確認入力]**  
 正しく入力されたことを確認するために、パスワードを再入力します。  
  
## <a name="see-also"></a>関連項目  
 [[ディストリビューションの構成]](configure-distribution.md)   
 [パブリッシングおよびディストリビューションの構成](configure-publishing-and-distribution.md)  
  
  
