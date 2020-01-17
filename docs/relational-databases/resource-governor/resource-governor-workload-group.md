---
title: リソース ガバナー ワークロード グループ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 4f15d4e443f0ffd6df700bff67ed6ba7514e0c90
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "68126879"
---
# <a name="resource-governor-workload-group"></a>リソース ガバナー ワークロード グループ
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] リソース ガバナーでは、ワークロード グループは分類基準が類似しているセッション要求のコンテナーとして機能します。 ワークロードは、セッションの全体的な監視を可能にし、セッションのポリシーを定義します。 各ワークロード グループはリソース プール内に存在します。リソース プールは [!INCLUDE[ssDE](../../includes/ssde-md.md)]インスタンスの物理リソースのサブセットを表します。 セッションの起動時に、リソース ガバナーの分類子によって、セッションは指定されたワークロード グループに割り当てられます。セッションの実行にはワークロード グループに割り当てられたポリシーおよびリソース プールに対して定義されたリソースを使用する必要があります。  
  
## <a name="workload-group-concepts"></a>ワークロード グループの概念  
 ワークロード グループは、分類基準を適用して類似すると判断されたセッション要求のコンテナーとして機能します。 ワークロード グループによって、リソース消費の全体的な監視、およびグループ内のすべての要求に対する一貫したポリシーの適用が可能となります。 グループは、そのメンバーに対するポリシーを定義します。  
  
> [!NOTE]  
>  ユーザー定義のワークロード グループは、リソース プール間で移動できます。  
  
 リソース ガバナーでは、内部グループと既定のグループの 2 つのワークロード グループが事前に定義されます。 内部グループとして分類されたグループは変更できませんが、監視することはできます。 次の条件に当てはまる場合は、要求が既定のグループへと分類されます。  
  
-   要求を分類する基準がない。  
  
-   要求を存在しないグループに分類しようとした。  
  
-   一般的な分類エラーが発生した。  
  
 リソース ガバナーには、ワークロード グループを作成、変更、および削除するための DDL ステートメントも用意されています。  
  
## <a name="workload-group-tasks"></a>ワークロード グループのタスク  
  
|タスクの説明|トピック|  
|----------------------|-----------|  
|ワークロード グループを作成する方法について説明します。|[ワークロード グループの作成](../../relational-databases/resource-governor/create-a-workload-group.md)|  
|ワークロード グループの設定を変更する方法について説明します。|[ワークロード グループの設定の変更](../../relational-databases/resource-governor/change-workload-group-settings.md)|  
|ワークロード グループを削除する方法について説明します。|[ワークロード グループの削除](../../relational-databases/resource-governor/delete-a-workload-group.md)|  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](../../relational-databases/resource-governor/resource-governor.md)   
 [リソース ガバナーの有効化](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [リソース ガバナー リソース プール](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [リソース ガバナーの分類子関数](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [テンプレートを使用してリソース ガバナーを構成する](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [リソース ガバナー プロパティの表示](../../relational-databases/resource-governor/view-resource-governor-properties.md)  
  
  
