---
title: CDC 用に SQL Server を準備する方法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: a327fa18-58f4-4e69-bb87-44faf47e20ef
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f13e8eae235eb040e92baa15247b6094e9aa1075
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294699"
---
# <a name="how-to-prepare-sql-server-for-cdc"></a>CDC 用に SQL Server を準備する方法

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Oracle CDC サービスでは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のすべてのターゲット インスタンスに MSXDBCDC データベースが含まれている必要があります。 このデータベースを作成するには、CDC Service 構成コンソールの "SQL Server の準備" アクションを使用します。このタスクは、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の各ターゲット インスタンスに対して一度だけ実行します。  
  
 次に、CDC Service 構成コンソールを使用して [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを Oracle Change Data Capture 用に準備する方法について説明します。 このプロセスによって、MSXDBCDC データベースが作成され、必要なテーブル、ストアド プロシージャ、およびその他のアーティファクトが定義されます。  
  
 Oracle CDC 用の SQL Server の準備は、Oracle CDC Service の管理者が実行します。 CDC Service の管理者ロールの詳細については、「 [User Roles](../../integration-services/change-data-capture/user-roles.md)」を参照してください。  
  
### <a name="to-enable-sql-server-for-cdc"></a>CDC 用に SQL Server を有効にするには  
  
1.  **[スタート]** メニューの **[CDC Service Configuration for Oracle]** をクリックします。  
  
2.  左ペインで **[ローカルの CDC Service]** を選択してから、 **[アクション]** ペインの **[SQL Server の準備]** をクリックします。  
  
     または、 **[ローカルの CDC Service]** を右クリックして **[SQLServer の準備]** をクリックします。  
  
3.  [Oracle CDC 用 SQL Server インスタンスの準備] ダイアログ ボックスに必要な情報を入力します。 このダイアログ ボックスに必要な情報を入力する方法については、「 [Prepare SQL Server for CDC](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)」を参照してください。  
  
     Oracle CDC 用に SQL Server インスタンスを準備するには、ログインが MSXDBCDC データベースに対する書き込み権限を持っている必要があります。 `sysasmin` ロールのメンバーなど、MSXDBCDC データベースに対する書き込み権限を持つログインの資格情報を入力します。  
  
 **注**: **[スクリプトの表示]** をクリックすると、セットアップ スクリプトの読み取り専用バージョンを表示できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のシステム管理者は、必要に応じて、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 管理コンソールにこのスクリプトをコピーして編集および実行することができます。  
  
## <a name="see-also"></a>参照  
 [CDC 用の SQL Server の準備](../../integration-services/change-data-capture/prepare-sql-server-for-cdc.md)  
  
  
