---
title: CDC 制御タスクのカスタム プロパティ | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 2a073699-79a2-4ea1-a68e-fc17a80b74ba
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 048cbe154dde064d43178da6c58e5f948130ca7b
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294270"
---
# <a name="cdc-control-task-custom-properties"></a>CDC 制御タスクのカスタム プロパティ

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  次の表は、CDC 制御タスクのカスタム プロパティを示しています。 すべてのプロパティは読み取り/書き込み可能です。  
  
|プロパティ名|データ型|[説明]|  
|-------------------|---------------|-----------------|  
|接続|ADO.NET Connection|変更テーブルおよび CDC 状態 (同じデータベースに格納されている場合) にアクセスするための、 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CDC データベースへの ADO.NET 接続。<br /><br /> 選択した変更テーブルが存在する、CDC に対応した [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースへの接続である必要があります。|  
|TaskOperation|Integer (列挙)|CDC 制御タスクに対して選択した操作。 有効な値は、 **[初期読み込みの開始をマーク]** 、 **[初期読み込みの終了をマーク]** 、 **[CDC の開始をマーク]** 、 **[処理範囲の取得]** 、 **[処理済みの範囲をマーク]** 、および **[CDC の状態をリセット]** です。<br /><br /> (Oracle ではなく) **CDC での作業時に**[MarkCdcStart] **、** [MarkInitialLoadStart] **、または** [MarkInitialLoadEnd] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] を選択した場合、接続マネージャーで指定されたユーザーは、  **db_owner** か **sysadmin**である必要があります。<br /><br /> これらの操作の詳細については、「 [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md) 」(CDC 制御タスク エディター) と「 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)」(CDC 制御タスク) を参照してください。|  
|OperationParameter|String|現在、 **MarkCdcStart** 操作で使用されています。 このパラメーターでは、特定の操作に必要な追加情報を入力できます。 たとえば、 **MarkCdcStart** 操作には LSN 番号が必要です。|  
|StateVariable|String|現在の CDC コンテキストの CDC の状態を格納する SSIS パッケージ変数。 **AutomaticStatePersistenceCDC** が選択されていない限り、制御タスクは **StateVariable** に対して状態を読み書きし、永続ストレージからの読み込みまたは格納は行いません。 「 [Define a State Variable](../../integration-services/data-flow/define-a-state-variable.md)」(状態変数の定義) を参照してください。|  
|StateVariable|Boolean|CDC 制御タスクは、CDC 状態パッケージ変数から CDC 状態を読み取ります。 操作後、CDC 制御タスクによって CDC 状態パッケージ変数の値が更新されます。 **AutomaticStatePersistence** プロパティによって、SSIS パッケージの実行間で CDC 状態値を保持する役割が、CDC 制御タスクに指示されます。<br /><br /> このプロパティが **true**の場合、CDC 制御タスクによって、CDC 状態変数の値が状態テーブルから自動的に読み込まれます。 CDC 制御タスクによって CDC 状態変数の値が更新されると、特別なテーブルの状態である、同じ状態 **table.stores**の値も更新され、状態変数が更新されます。 開発者は、状態テーブルとその名前を保存する [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースを制御できます。 この状態テーブルの構造はあらかじめ定義されています。<br /><br /> **false**の場合、CDC 制御タスクはその値の保持に関する処理を行いません。 true の場合、CDC 制御タスクが特別なテーブルに状態を格納し、StateVariable を更新します。<br /><br /> 既定値は **true**で、状態の保持が自動的に更新されることを示します。|  
|StateConnection|ADO.NET Connection|**AutomaticStatePersistence**を使用する場合に、状態テーブルが存在するデータベースへの ADO.NET 接続。 既定値は、 **Connection**と同じ値です。|  
|StateName|String|永続的な状態に関連付ける名前です。 同じ CDC コンテキストを使用する完全読み込みパッケージと CDC パッケージでは、共通の CDC コンテキスト名を指定する必要があります。 この名前は、状態テーブルで状態行を検索するために使用されます。<br /><br /> このプロパティは、 **AutomaticStatePersistence** を **true**に設定する場合のみ適用されます。|  
|StateTable|String|CDC のコンテキスト状態が格納されているテーブルの名前を指定します。 このテーブルは、このコンポーネントに対して構成されている接続を使用してアクセスする必要があります。 このテーブルには、 **name** および **state**という名前の varchar 列が必要です ( **state** 列は少なくとも 256 文字であることが必要です)。<br /><br /> このプロパティは、 **AutomaticStatePersistence** を **true**に設定する場合のみ適用されます。|  
|CommandTimeOut|整数 (integer)|この値は、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] データベースと通信する際に使用されるタイムアウト (秒単位) を示します。 この値は、データベースからの応答時間が非常に遅い場合に使用されるため、既定値 (30 秒) では不十分です。|  
  
## <a name="see-also"></a>参照  
 [CDC Control Task](../../integration-services/control-flow/cdc-control-task.md)   
 [CDC Control Task Editor](../../integration-services/control-flow/cdc-control-task-editor.md)  
  
  
