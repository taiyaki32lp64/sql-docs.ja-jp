---
title: "ディストリビューターでのリモート パブリッシャーの有効化 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- remote Distributors [SQL Server replication]
- Publishers [SQL Server replication]
ms.assetid: 6f8e2831-5c45-4e39-8e51-d37e2813cf3d
caps.latest.revision: 30
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 848c1142c1db178efe9215db06fd326ea4aade6e
ms.contentlocale: ja-jp
ms.lasthandoff: 06/22/2017

---
# <a name="enable-a-remote-publisher-at-a-distributor-sql-server-management-studio"></a>ディストリビューターでのリモート パブリッシャーの有効化 (SQL Server Management Studio)
  **[パブリッシャー]** ページでパブリッシャーを有効にし、リモート ディストリビューターを使用します。 このページは、ディストリビューションの構成ウィザードおよび **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスにあります。 ウィザードとダイアログ ボックスのアクセス方法については、「[パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)」と「[ディストリビューターとパブリッシャーのプロパティの表示および変更](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)」を参照してください。  
  
### <a name="to-enable-a-publisher-in-the-configure-distribution-wizard"></a>ディストリビューションの構成ウィザードでパブリッシャーを有効にするには  
  
1.  ディストリビューションの構成ウィザードの **[パブリッシャー]** ページで、 **[追加]**をクリックします。  
  
2.  **[SQL Server パブリッシャーの追加]**をクリックします。 Oracle パブリッシャーを有効にしてディストリビューターを使用する方法については、「 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」を参照してください。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、リモート ディストリビューターを使用するパブリッシャーの接続情報を指定し、 **[接続]**をクリックします。  
  
4.  **[ディストリビューター パスワード]** ページの **[パスワード]** テキスト ボックスおよび **[パスワードの確認入力]** テキスト ボックスで、 **distributor_admin** アカウントの複雑なパスワードを指定します。レプリケーションでは、このアカウントを使用してパブリッシャーからディストリビューターに接続し、管理タスクを実行します。  
  
5.  パブリッシャーの設定を表示および変更するには、プロパティ ボタン (**[...]**) をクリックします。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-enable-a-publisher-in-the-distributor-properties-dialog-box"></a>[ディストリビューターのプロパティ] ダイアログ ボックスでパブリッシャーを有効にするには  
  
1.  **[ディストリビューターのプロパティ - \<Distributor>]** ダイアログ ボックスの **[パブリッシャー]** ページで、**[追加]** をクリックします。  
  
2.  **[SQL Server パブリッシャーの追加]**をクリックします。 Oracle パブリッシャーを有効にしてディストリビューターを使用する方法については、「 [Create a Publication from an Oracle Database](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)」を参照してください。  
  
3.  **[サーバーへの接続]** ダイアログ ボックスで、リモート ディストリビューターを使用するパブリッシャーの接続情報を指定し、 **[接続]**をクリックします。  
  
4.  **[パブリッシャー]** ページの **[パスワード]** テキスト ボックスおよび **[パスワードの確認入力]** テキスト ボックスで、 **distributor_admin** アカウントの複雑なパスワードを指定します。レプリケーションでは、このアカウントを使用してパブリッシャーからディストリビューターに接続し、管理タスクを実行します。  
  
5.  パブリッシャーの設定を表示および変更するには、プロパティ ボタン (**[...]**) をクリックします。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>参照  
 [パブリッシングおよびディストリビューションの構成](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [[ディストリビューションの構成]](../../relational-databases/replication/configure-distribution.md)   
 [ディストリビューターのセキュリティ保護](../../relational-databases/replication/security/secure-the-distributor.md)  
  
  