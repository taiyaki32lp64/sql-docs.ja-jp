---
title: Azure Storage への接続 (復元) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.restore.connectstorage.f1
ms.assetid: c0b7d7c8-b878-4b7f-8120-d0c6917b583f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6fbb57fe629797e34cc7c61f224d65d46d4e66cd
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154771"
---
# <a name="connect-to-azure-storage-restore"></a>Azure Storage への接続 (復元)
  このダイアログボックスでは、azure ストレージアカウントのファイルストレージを取得するために、Azure storage アカウント情報への接続を指定できます。 必要な情報を指定したら、 **[接続]** をクリックして Azure storage への接続を確立します。  
  
## <a name="azure-storage-account"></a>Azure ストレージ アカウント  
 **[ストレージ アカウント]**  
 使用する Azure ストレージアカウントの名前を選択、入力、または貼り付けます。 ドロップダウン リストに、以前に使用したアカウントが表示されます。  
  
 **アカウント キー**  
 Azure ストレージアカウントのアクセスキーを指定します。  
  
 **[安全なエンドポイントを使用する (HTTPS)]** チェック ボックス  
 Azure storage へのセキュリティで保護された接続を行うには、このオプションを選択します。  
  
 **[アカウント キーを保存する]** チェック ボックス  
 このストレージ アカウントのアクセス キーを SQL Server に記憶させる場合は、このチェック ボックスをオンにします。  
  
### <a name="sql-credential"></a>[SQL 資格情報]  
 **[既存の資格情報の選択]**  
 ストレージ アカウントおよびアカウント キー情報と一致する既存の SQL 資格情報を選択します。  
  
 **[新しい資格情報の作成]**  
 ストレージ アカウントとアカウント キー情報を使用して新しい資格情報を作成するには、このオプションを選択します。 **[資格情報名]** フィールドに新しい資格情報の名前を指定します。  
  
  
