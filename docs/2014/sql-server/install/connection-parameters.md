---
title: 接続パラメーター |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server], connections
- authentication [Upgrade Advisor]
- SQL Server Upgrade Advisor, connections
- connections [Upgrade Advisor]
- server instances [Upgrade Advisor]
- default server instances
- analyzing system [Upgrade Advisor], connections
ms.assetid: f754d038-637a-4d8e-85b0-b242e6499d26
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca5d6ed8f1e8a92d22bd32e39c8afe946a0fcfee
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095975"
---
# <a name="connection-parameters"></a>接続パラメーター
  [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]など、特定の種類のサーバーを分析するには、[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の特定のインスタンスを選択する必要があります。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の既定のインスタンスは自動的に選択されます。 この選択は変更できますが、アップグレード アドバイザーによる分析用に選択できるのは一度に 1 つのインスタンスだけです。 認証が必要なサーバーを選択した場合は、認証モードと資格情報を入力する必要があります。  
  
## <a name="options"></a>および  
 **サーバー名**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント ペインに入力したコンピューター名が自動的に表示されます。  
  
 **インスタンス名**  
 コンピューターで使用可能な [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のインスタンスから選択します。 インスタンスの一覧が表示されない場合は、MSSQLSERVER を使用して、既定のインスタンスをスキャンします。 これは、特にリモート コンピューターに関連します。 「default」と入力して、既定のインスタンスをスキャンすることもできます。  
  
 **[認証]**  
 このコンピューターで使用できる認証モードの一覧から選択します。 既定の認証モードは Windows 認証です。  
  
 **ユーザー名**  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 認証を使用する場合は、このボックスにユーザー名を入力します。 ここには、コンピューターの管理者の資格情報を持っているユーザー名を入力することをお勧めします。  
  
> [!NOTE]  
>  現在ログオンしているユーザーのユーザー名が入力されて Windows 認証を選択した場合、**ユーザー名**テキスト ボックス。  
  
 **Password**  
 指定したユーザーのパスワードを入力します。  
  
## <a name="see-also"></a>参照  
 [アップグレード アドバイザーの使用](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [アップグレード アドバイザーのユーザー インターフェイス リファレンス](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
