---
title: Oracle への接続 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- connOra
ms.assetid: 711ac7ff-5d3d-4533-80ca-d1fecdb3048f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e745a2277a01cac3dd120af241e0ae1d7575b562
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294747"
---
# <a name="connect-to-oracle"></a>Oracle への接続

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  CDC インスタンスに使用するテーブルを初めて追加または編集するとき、Oracle データベースへの接続を要求されることがあります。 キャプチャするテーブルのスキーマにアクセスできる Oracle ユーザーの資格情報を入力する必要があります。 このダイアログ ボックスでは次の情報を入力します。  
  
 **[認証]**  
  
 次のいずれかを選択します。  
  
-   **[Windows 認証]** :現在の Windows ドメイン資格情報を使用する場合に選択します。 このオプションは、Oracle データベースが Windows 認証と連動するように構成されている場合にのみ使用できます。  
  
-   **[Oracle 認証]** :このオプションを選択する場合、接続先の Oracle データベースのユーザーの **[ユーザー名]** と **[パスワード]** を入力する必要があります。  
  
## <a name="see-also"></a>参照  
 [CDC へのテーブルの追加](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)  
  
  
