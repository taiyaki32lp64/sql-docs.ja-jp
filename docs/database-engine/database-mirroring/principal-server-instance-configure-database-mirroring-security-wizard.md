---
title: '[プリンシパル サーバー インスタンス] (データベース ミラーリング セキュリティ構成ウィザード)'
description: SQL Server Management Studio のデータベース ミラーリング セキュリティ構成ウィザードの [プリンシパル サーバー インスタンス] ページの説明です。
ms.custom: seo-lt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.configdbmsecurwiz.principalsrvr.f1
ms.assetid: 58af27d7-c5dd-4669-be6b-b472bc2c8ef4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 8d48c59b06202f898fdf61746aee9f62ca155da6
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255961"
---
# <a name="principal-server-instance-configure-database-mirroring-security-wizard"></a>[プリンシパル サーバー インスタンス] (データベース ミラーリング セキュリティ構成ウィザード)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  このページを使用すると、プリンシパル データベースのサーバー インスタンスに関する情報を指定できます。 プリンシパル データベースは、ミラーリング セッションを開始するデータベースのコピーです。 セッションが開始された後は、プリンシパル データベースは、ユーザーが変更できるデータベースのコピーになります。 フェールオーバーが発生するとプリンシパル ロールとミラーリング ロールが入れ替わるため、最初のプリンシパル データベースが途中でプリンシパル データベースでなくなる可能性があります。  
  
 **SQL Server Management Studio を使用してデータベース ミラーリングを構成するには**  
  
-   [Windows 認証を使用してデータベース ミラーリング セッションを確立する &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/establish-database-mirroring-session-windows-authentication.md)  
  
-   [データベース ミラーリング セキュリティ構成ウィザードの起動 &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/start-the-configuring-database-mirroring-security-wizard.md)  
  
## <a name="options"></a>オプション  
 **[プリンシパル サーバー インスタンス]**  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のデータベース ミラーリングは常にプリンシパル サーバーから構成されるため、必ず現在のサーバー インスタンスがプリンシパル サーバー インスタンスになります。  
  
 **リスナー ポート**  
 このオプションでは、このサーバー インスタンスに対するミラーリング エンドポイントが存在するかどうかに応じて、次のような内容が表示されます。  
  
-   このサーバー インスタンスに対するリスナー ポートが存在しない場合、 **[ポート]** テキスト ボックスにポート番号 5022 が表示されます。 使用可能な任意のポート番号を入力できます (7022 など)。  
  
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
  
  
