---
title: 資格情報の作成- Azure ストレージに対する認証 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql12.swb.backuptourl.createcred.f1
ms.assetid: 0622619d-27c5-4ff0-83e5-cde31648c27a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6de7b5c8f9cdc7162eb9c6a8ddd214d0486255c6
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175956"
---
# <a name="create-credential---authenticate-to-azure-storage"></a>資格情報の作成- Azure ストレージに対する認証
  **[Backup To URL - 資格情報の作成]** ダイアログ ボックスを使用すると、新しい SQL 資格情報を作成できます。  
  
 このダイアログボックスを使用して資格情報を作成する場合は、ローカルの証明書ストアに追加された Azure 管理証明書、またはコンピューターにダウンロードした発行プロファイルを指定して、サブスクリプションとストレージアカウント情報を検証する必要があります。  
  
 **[SQL 資格情報]**  
 作成する SQL 資格情報の名前を指定します。  
  
## <a name="azure-credentials"></a>Azure の資格情報  
 **[管理証明書]**  
 このオプションを使用して、Azure の管理証明書に一致するローカル証明書ストアの証明書を指定します。 Azure 管理証明書の詳細については、「 [azure の管理証明書の作成とアップロード](https://go.microsoft.com/fwlink/?LinkId=320781)」を参照してください。  
  
 **サブスクリプション**  
 ローカル証明書ストアの管理証明書と一致する Azure サブスクリプション ID を選択、入力、または貼り付けます。  
  
 **[公開プロファイル]**  
 コンピューターにダウンロードした公開プロファイルがある場合は、このオプションを使用します。 このオプションを使用すると、サブスクリプション ID と証明書が自動的に入力されます。  
  
> [!CAUTION]  
>  SQL Server では現在、公開プロファイルのバージョン 2.0 がサポートされています。 公開プロファイルのサポート対象バージョンをダウンロードするには、「 [公開プロファイルのバージョン 2.0 のダウンロード](https://go.microsoft.com/fwlink/?LinkId=396421)」をご覧ください。  
  
## <a name="storage-account"></a>ストレージ アカウント  
 バックアップ ファイルを格納するために使用するストレージ アカウントを選択します。  
  
  
