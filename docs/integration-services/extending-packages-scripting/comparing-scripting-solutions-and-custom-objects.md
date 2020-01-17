---
title: スクリプティング ソリューションとカスタム オブジェクトとの比較 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- managed tasks [Integration Services]
- Script task [Integration Services], vs. custom managed tasks
- SSIS Script task, vs. custom managed tasks
- custom tasks [Integration Services], scripts
ms.assetid: c0aea822-a21e-44e1-a3d3-8777bd0a1c34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 492f5e288faaedda21dc529fdfeeda6006d78b12
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71286456"
---
# <a name="comparing-scripting-solutions-and-custom-objects"></a>スクリプティング ソリューションとカスタム オブジェクトとの比較

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] スクリプト タスクまたはスクリプト コンポーネントは、カスタム マネージド タスクまたはデータ フロー コンポーネントで使用できる機能とほぼ同じ機能を実装できます。 ここでは、適切な種類のタスクを必要に応じて選択するときに役立つ注意事項について説明します。  
  
-   構成または機能が個々のパッケージに固有である場合は、カスタム オブジェクトを開発する代わりに、スクリプト タスクまたはスクリプト コンポーネントを使用します。  
  
-   機能が汎用で、将来は他のパッケージ用に使用されたり、他の開発者が使用する可能性がある場合は、スクリプト ソリューションを使用する代わりに、カスタム オブジェクトを作成します。 カスタム オブジェクトは任意のパッケージで使用できますが、スクリプトは、そのスクリプトが作成されたパッケージでのみ使用できます。  
  
-   同じパッケージ内でコードを再使用する場合、カスタム オブジェクトを作成することを検討します。 あるスクリプト タスクまたはコンポーネントから別のスクリプト タスクまたはコンポーネントにコードをコピーすると、コードの複数コピーの維持および更新が煩雑になるため、管理が難しくなります。  
  
-   将来的に実装方法を変更する場合は、カスタム オブジェクトの使用を検討します。 カスタム オブジェクトは、親パッケージとは別に開発および配置できますが、スクリプト ソリューションを更新する場合は、パッケージ全体を再配置する必要があります。  
  
## <a name="see-also"></a>参照  
 [カスタム オブジェクトを使用したパッケージの拡張](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
  
  
