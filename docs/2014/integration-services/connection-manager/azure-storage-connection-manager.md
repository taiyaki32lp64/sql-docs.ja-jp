---
title: Azure Storage 接続マネージャー | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea689f96911af35176d6467e73d496b59f35e3c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "62833560"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage 接続マネージャー
  Azure Storage 接続マネージャーでは、プロパティを指定する値を使用して、Azure Storage アカウントに接続する SSIS パッケージが有効にします。接続することを可能にします。  
  
1.  **[SSIS 接続マネージャーの追加]** ダイアログ ボックスで **[AzureStorage]** (AzureStorage) を選択し、 **[追加]** をクリックします。  
  
2.  Azure Storage 接続マネージャー エディター ダイアログ ボックスで、インターネット経由で Azure Storage サービスに接続する場合は **[Use Azure account]** (Azure アカウントを使用する) を選択し、Azure Storage エミュレーターによってホストされているローカル サービスに接続する場合は **[Use local developer account]** (ローカル開発者アカウントを使用する) を選択します。  
  
3.  **[Use Azure account]** (Azure アカウントを使用する) オプションを選択した場合は、次の操作を行います。  
  
    1.  **[Storage account name]** (ストレージ アカウント名) フィールドと **[Account key]** (アカウント キー) フィールドに値を指定します。 これらの値は、SSIS パッケージ内で機微なデータとして保存されます。  
  
    2.  Azure Storage サービスへの接続に HTTP ではなく HTTPS を使用する場合は、 **[Use HTTPS]** (HTTPS を使用する) を選択します。  
  
4.  **[OK]** をクリックしてダイアログ ボックスを閉じます。  
  
5.  作成した接続マネージャーのプロパティは、 **[プロパティ]** ウィンドウに表示されます。  
  
  
