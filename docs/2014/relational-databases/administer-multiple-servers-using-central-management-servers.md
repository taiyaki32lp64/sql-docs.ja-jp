---
title: 中央管理サーバーを使用した複数のサーバーの管理 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- multiserver queries
- central management server
- multiserver administration [SQL Server]
- master servers [SQL Server], central management servers
- target configuration [SQL Server]
- server configuration [SQL Server]
ms.assetid: 427911a7-57d4-4542-8846-47c3267a5d9c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f47eec543c21e74565d750035d20fbcee9baa82e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62877312"
---
# <a name="administer-multiple-servers-using-central-management-servers"></a>中央管理サーバーを使用した複数のサーバーの管理
  中央管理サーバーを指定し、サーバー グループを作成することで、複数のサーバーを管理できます。  
  
## <a name="benefits-of-central-management-servers-and-server-groups"></a>中央管理サーバーとサーバー グループの利点  
 中央管理サーバーとして指定した [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] のインスタンスによってサーバー グループが管理され、サーバー グループによって [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] の 1 つ以上のインスタンスの接続情報が管理されます。 サーバー グループに対しては、[!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントおよびポリシー ベースの管理ポリシーを同時に実行できます。 中央管理サーバーを通じて管理されているインスタンスの [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ログ ファイルを表示することもできます。 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] よりも前のバージョンの [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] では、中央管理サーバーを指定できません。  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] ステートメントは、登録済みサーバー内のローカル サーバー グループに対しても実行できます。  
  
### <a name="related-tasks"></a>Related Tasks  
 中央管理サーバーとサーバー グループを作成するには、[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] の **[登録済みサーバー]** ウィンドウを使用します。 中央管理サーバーを、それ自体が管理するグループのメンバーにすることはできません。 中央管理サーバーとサーバー グループの作成方法については、「[中央管理サーバーおよびサーバー グループの作成 &#40;SQL Server Management Studio&#41;](../ssms/register-servers/create-a-central-management-server-and-server-group.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ポリシー ベースの管理を使用したサーバーの管理](policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
