---
title: HOST_NAME 値 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newsubwizard.hostnamevalue.f1
ms.assetid: 21548f08-2910-4a55-baac-b911ba9afaf1
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3bcfcf089d8a50f9b94498cc68f12a4d6f0ac97f
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770622"
---
# <a name="hostname-values"></a>[HOST_NAME 値]
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

パラメーター化されたフィルター付きのマージ パブリケーションは、SUSER_SNAME() 関数または HOST_NAME() 関数を使用してデータにフィルターをかけます。 関数は、パブリケーションの新規作成ウィザードまたは **[パブリケーションのプロパティ]** ダイアログ ボックスで指定します。  
  
既定では、HOST_NAME() 関数は、パブリッシャーに接続しているコンピューターの名前を返します。 通常、パラメーター化されたフィルターを使用する場合は、ウィザードのこのページで値を指定してこの値をオーバーライドします。 これにより、HOST_NAME() 関数は、コンピューターの名前ではなく、指定された値を返します。 詳細については、「[Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)」 (パラメーター化された行フィルター) の "Overriding the HOST_NAME() Value" (HOST_NAME() 値のオーバーライド) をご覧ください。  
  
> [!NOTE]  
>  HOST_NAME() をオーバーライドした場合、HOST_NAME() 関数のすべての呼び出しは、指定された値を返します。 他のアプリケーションが、コンピューター名を返す HOST_NAME() 関数に依存していないことを確認してください。  
  
## <a name="options"></a>オプション  
 **[サブスクリプションのプロパティ]**  
 サブスクライバーごとに **[HOST_NAME 値]** 列に値を入力するか、既定値を受け入れます。既定値は、サブスクライバー コンピューターの名前です。  
  
## <a name="see-also"></a>参照  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [ssSDSFull](../../relational-databases/replication/create-a-push-subscription.md)   
 [プル サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)   
 [プッシュ サブスクリプションのプロパティの表示または変更](../../relational-databases/replication/view-and-modify-push-subscription-properties.md)   
 [HOST_NAME (Transact-SQL)](../../t-sql/functions/host-name-transact-sql.md)   
 [パブリケーションのサブスクライブ](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
