---
title: 接続済みサーバーの登録
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerserver.f1
helpviewer_keywords:
- Registered Servers [SQL Server], register connected servers
- connected server registrations [SQL Server]
ms.assetid: 77deb5f5-0f80-484f-8b8b-29afa67ec18f
author: markingmyname
ms.author: maghan
manager: jroth
ms.openlocfilehash: adb411df9f1a67b3c8963382f0c907e04c395b5b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75241336"
---
# <a name="register-a-connected-server-sql-server-management-studio"></a>接続済みのサーバーの登録 (SQL Server Management Studio)
  このトピックでは、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] を使用して、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]でサーバーを登録する方法について説明します。 サーバーを登録することによって、頻繁にアクセスするサーバーの接続情報を保存しておくことができます。 サーバーの登録は、接続する前か、またはオブジェクト エクスプローラーから接続するときに実行できます。  
  
 **このトピックの内容**  
  
-   **サーバーを登録するために使用するもの:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="SSMSProcedure"></a>SQL Server Management Studio の使用  
  
#### <a name="to-register-a-connected-server"></a>接続済みのサーバーを登録するには  
  
1.  オブジェクト エクスプローラーで、接続済みのサーバーを右クリックし、 **[登録]** をクリックします。  
  
     **サーバー名**  
     登録するサーバーに使用する名前を入力します。 
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] を使用してローカル サーバーまたはリモート サーバーを登録することにより、以降の接続で使用するサーバー接続情報を格納できます。 このフィールドの既定値は、サーバーに接続したときに入力したサーバー名です。 このサーバー名を維持するか、別の使いやすい名前を入力します。  
  
     **[サーバーの説明]**  
     サーバーの説明をオプションで入力します。 最大 250 文字以内で指定します。  
  
     **[サーバー グループの選択]**  
     サーバー登録を保存するサーバー グループを選択します。  
  
     **新しいグループ**  
     クリックすると、登録するサーバー用の新しいサーバー グループを作成するための **[新しいグループ]** ダイアログ ボックスが開きます。  
  
     **保存**  
     クリックすると、入力した情報を保存して登録済みサーバーを作成できます。  
  
  
