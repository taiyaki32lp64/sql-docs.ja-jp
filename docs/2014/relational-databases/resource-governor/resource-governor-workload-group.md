---
title: リソース ガバナー ワークロード グループ | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, workload group
- workload groups [SQL Server]
- workload groups [SQL Server], overview
ms.assetid: a84c3c3f-55b6-4a30-9c42-13f082d9281e
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: de33dafe9c2274e8e016d619c1e7b5762d73e7aa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209706"
---
# <a name="resource-governor-workload-group"></a>リソース ガバナー ワークロード グループ
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
|ワークロード グループを作成する方法について説明します。|[ワークロード グループの作成](create-a-workload-group.md)|  
|ワークロード グループの設定を変更する方法について説明します。|[ワークロード グループの設定の変更](change-workload-group-settings.md)|  
|ワークロード グループを削除する方法について説明します。|[ワークロード グループの削除](delete-a-workload-group.md)|  
  
## <a name="see-also"></a>参照  
 [リソース ガバナー](resource-governor.md)   
 [リソース ガバナーの有効化](enable-resource-governor.md)   
 [リソース ガバナー リソース プール](resource-governor-resource-pool.md)   
 [リソース ガバナーの分類子関数](resource-governor-classifier-function.md)   
 [テンプレートを使用してリソース ガバナーを構成する](configure-resource-governor-using-a-template.md)   
 [リソース ガバナー プロパティの表示](view-resource-governor-properties.md)  
  
  
