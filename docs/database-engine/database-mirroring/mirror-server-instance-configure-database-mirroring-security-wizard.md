---
title: 'セキュリティの構成ウィザード: ミラー サーバー インスタンス'
description: SQL Server Management Studio の [データベース ミラーリング セキュリティ構成ウィザード] の [ミラー サーバー インスタンス] ページについて説明します。
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.mirrorsrvr.f1
ms.assetid: 53223432-615e-440f-904d-925d33ec2144
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d52fa3912bffd084a8f95e79963abcd99158cdd4
ms.sourcegitcommit: f8cf8cc6650a22e0b61779c20ca7428cdb23c850
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74822397"
---
# <a name="configure-database-mirrroing-security-wizard-mirror-server-instance"></a>データベース ミラーリング セキュリティ構成ウィザード: ミラー サーバー インスタンス
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、ミラー データベースを持つサーバー インスタンスに関する情報を指定できます。  
  
> [!IMPORTANT]  
>  ミラー サーバー インスタンスでは、プリンシパル サーバー インスタンスと同じ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]のエディション (Standard または Enterprise) を実行している必要があります。 また、ワークロードの処理能力が同程度のシステム上で運用することを強くお勧めします。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>オプション  
 **[ミラー サーバー インスタンス]**  
 **[データベースのプロパティ]** ダイアログ ボックスの **[ミラー化]** ページで、ミラー サーバー インスタンスが既に指定されている場合、そのインスタンスが表示されます。詳細については、「[[データベースのプロパティ] &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)」を参照してください。  
  
 まだ指定されていない場合は、ミラー サーバー インスタンスの名前を入力します。 プリンシパル サーバー インスタンスと同じ名前をミラー サーバー インスタンスに指定しないように注意してください。  
  
 **のインスタンスに接続するときには、**  
 ミラー サーバー インスタンスが指定されていない場合、 **[接続]** をクリックします。 **[サーバーへの接続]** ダイアログ ボックスが表示されます。ここでサーバー インスタンスを指定し、接続を確立できます。  
  
 インスタンスが指定されていても、エンドポイントが存在するかどうかをチェックできる権限を持つ接続がない場合には、 **[接続]** をクリックします。 **[サーバーへの接続]** ダイアログ ボックスが表示されます。この場合、サーバー インスタンスは選択されており、変更できません。 十分な権限を持つドメイン アカウントを指定して、サーバー インスタンスに接続します。  
  
> [!NOTE]  
>  データベース ミラーリング セキュリティ構成ウィザードは、 **[サーバーへの接続]** ダイアログ ボックスで指定された資格情報を使ってサーバー インスタンスに接続します。 これらは、ミラーリング セッションの資格情報とは異なります。ミラーリング セッションでは、サーバー インスタンスをサービスとして実行している開始アカウントの資格情報が使用されます。  
  
 **リスナー ポート**  
 このオプションでは、このサーバー インスタンスに対するミラーリング エンドポイントが存在するかどうかに応じて、次のような内容が表示されます。  
  
-   サーバー インスタンスに対するリスナー ポートが存在しない場合、 **[リスナー ポート]** テキスト ボックスにポート番号 5022 が表示されます。 使用可能な任意のポート番号を入力できます (7022 など)。  
  
-   ミラーリング エンドポイントが既に存在する場合、そのエンドポイントからのポート番号が表示されます。 ポートを変更する必要がある場合は、ALTER ENDPOINT コマンドを使用します。 詳細については、「 [ALTER ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/alter-endpoint-transact-sql.md)」を参照してください。  
  
    > [!NOTE]  
    >  ポート番号は必須です。  
  
 **[エンドポイント名]**  
 このサーバー インスタンスのミラーリング エンドポイントが存在する場合、ここにエンドポイント名が表示されます。 エンドポイントが存在しない場合には、エンドポイントの名前を指定できます。  
  
 **[このエンドポイントから送られるデータを暗号化する]**  
 既定で、暗号化は有効になっています。 暗号化が有効な場合、暗号化は必須です (サポートされるだけではありません)。暗号化オプションにはすべて既定値が使用されます。 詳細については、「[CREATE ENDPOINT &#40;Transact-SQL&#41;](../../t-sql/statements/create-endpoint-transact-sql.md)」を参照してください。  
  
 暗号化を無効にするには、チェック ボックスをオフにします。 暗号化を再度有効にするには、チェック ボックスをオンにします。  
  
## <a name="see-also"></a>参照  
 [データベース ミラーリング エンドポイント &#40;SQL Server&#41;](../../database-engine/database-mirroring/the-database-mirroring-endpoint-sql-server.md)   
 [データベース プロパティ &#40;[ミラーリング] ページ&#41;](../../relational-databases/databases/database-properties-mirroring-page.md)   
 [Windows 認証でのデータベース ミラーリング エンドポイントの作成 &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)   
 [データベース ミラーリング モニターの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-database-mirroring-monitor-sql-server-management-studio.md)   
 [データベース ミラーリング &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
