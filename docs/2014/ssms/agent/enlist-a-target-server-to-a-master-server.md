---
title: マスター サーバーへのターゲット サーバーの参加 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- enlisting target servers [SQL Server]
- SQL Server Agent jobs, target servers
- master servers [SQL Server], enlisting target servers
- SQL Server Agent jobs, master servers
- target servers [SQL Server], enlisting
ms.assetid: 7633adb5-d140-4e58-a8f2-5b4b50c2f95b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f3d0d91de95e82fcd174aa9290e208afda5bef91
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "68211395"
---
# <a name="enlist-a-target-server-to-a-master-server"></a>マスター サーバーへのターゲット サーバーの参加
  このトピックでは、マルチサーバー管理構成にターゲット サーバーを参加させる方法について説明します。 この手順はマスター サーバーから実行します。 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] で、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]、 [!INCLUDE[tsql](../../includes/tsql-md.md)]、または SQL Server 管理オブジェクト (SMO) を使用します。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] エージェント サービス用に使用される Windows アカウントがマルチサーバー環境に与える影響については、「 [マルチサーバー環境の作成](create-a-multiserver-environment.md)」を参照してください。  
  
 マスター サーバーとターゲット サーバーの間の接続では、完全な Secure Sockets Layer (SSL) 暗号化と証明書の検証が既定で有効になります。 詳しくは、「[ターゲット サーバーでの暗号化オプションの設定](set-encryption-options-on-target-servers.md)」をご覧ください。  
  
 **このトピックの内容**  
  
-   **対象サーバーを参加させるために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [SMO](#PowerShellProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio の使用  
  
#### <a name="to-enlist-a-target-server"></a>ターゲット サーバーを参加させるには  
  
1.  **オブジェクト エクスプローラー**で、マスター サーバーとして構成するサーバーを展開します。  
  
2.  **[SQL Server エージェント]** を右クリックし、 **[マルチ サーバーの管理]** をポイントして **[対象サーバーの追加]** をクリックします。  
  
3.  ターゲット サーバー設定ウィザードを実行し、指示に従って操作します。  
  
##  <a name="TsqlProcedure"></a> Transact-SQL の使用  
  
#### <a name="to-enlist-a-target-server"></a>ターゲット サーバーを参加させるには  
  
1.  `sp_msx_enlist` ストアド プロシージャを使用します。  詳細については、次を参照してください[sp_msx_enlist &#40;TRANSACT-SQL。&#41;](/sql/relational-databases/system-stored-procedures/sp-msx-enlist-transact-sql)  
  
##  <a name="PowerShellProcedure"></a> SQL Server 管理オブジェクト (SMO) の使用  
  
## <a name="see-also"></a>参照  
 [エンタープライズ全体の管理の自動化](automated-administration-across-an-enterprise.md)  
  
  
