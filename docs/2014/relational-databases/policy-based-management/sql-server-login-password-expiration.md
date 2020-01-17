---
title: SQL Server ログイン パスワードの有効期限 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7e3bf9da-a436-433d-847a-47c30428cad3
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: fda81a7774da697b3369efdd91d79d1f4dce00de
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63253437"
---
# <a name="sql-server-login-password-expiration"></a>SQL Server ログイン パスワードの有効期限
  このルールでは、各 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインの "パスワードの有効期限" が有効になっているかどうかを確認します。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が有効で、オペレーティング システムが [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]よりも前のバージョンである場合、攻撃者は既知の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログイン パスワードを繰り返し利用できます。  
  
## <a name="best-practices-recommendations"></a>ベスト プラクティスと推奨事項  
 オペレーティング システムを [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]にアップグレードすることをお勧めします。  
  
 使用している環境で [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証が必要ではない場合は、Windows 認証を使用します。 詳細については、「 [認証モードの選択](../security/choose-an-authentication-mode.md)」を参照してください。  
  
 すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ログインに対して、"パスワードの有効期限" を有効にします。 [ログインのパスワード ポリシーを構成するには、](/sql/t-sql/statements/alter-login-transact-sql) ALTER LOGIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を使用します。  
  
## <a name="for-more-information"></a>詳細情報  
 [パスワード ポリシー](../security/password-policy.md)  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したベスト プラクティスの監視と実行](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
