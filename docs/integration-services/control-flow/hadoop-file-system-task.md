---
title: Hadoop ファイル システム タスク | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hadoopfiletask.f1
ms.assetid: 594aaf5d-7703-4788-897d-fb95aca798c5
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e97ae33bcccee338be576138ca335bd6298e0128
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294067"
---
# <a name="hadoop-file-system-task"></a>Hadoop ファイル システム タスク

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Hadoop ファイル システム タスクを使用すると、SSIS パッケージで Hadoop クラスター内外にファイルをコピーできます。  
  
 Hadoop ファイル システム タスクを追加するには、デザイナーにドラッグ アンド ドロップします。 その後、タスクをダブルクリックするか、右クリックして **[編集]** をクリックし、 **[Hadoop ファイル システム タスク エディター]** ダイアログ ボックスを開きます。  
  
 ![[Hadoop ファイル システム タスク エディター]](../../integration-services/control-flow/media/hadoop-filesystem-task.png "[Hadoop ファイル システム タスク エディター]")  
  
## <a name="options"></a>オプション  
 **[Hadoop ファイル システム タスク エディター]** ダイアログ ボックスで、次のオプションを構成します。  
  
|フィールド|[説明]|  
|-----------|-----------------|  
|**Hadoop 接続**|既存の Hadoop 接続マネージャーを指定するか、新しい Hadoop 接続マネージャーを作成します。 この接続マネージャーは、対象ファイルがホストされる場所を示します。|  
|**[Hadoop File Path] (Hadoop ファイル パス)**|HDFS 上のファイルまたはディレクトリのパスを指定します。|  
|**[Hadoop File Type] (Hadoop ファイルの種類)**|HDFS ファイル システム オブジェクトがファイルまたはディレクトリのどちらであるかを指定します。|  
|**[変換先を上書き]**|対象ファイルが既に存在する場合に、そのファイルを上書きするかどうかを指定します。|  
|**操作**|操作を指定します。 **CopyToHDFS**、 **CopyFromHDFS**、および **CopyWithinHDFS**を指定できます。|  
|**[Local File Connection] (ローカル ファイル接続)**|既存のファイル接続マネージャーを指定するか、新しいファイル接続マネージャーを作成します。 この接続マネージャーは、ソース ファイルがホストされる場所を示します。|  
|**[Is Recursive] (再帰的)**|すべてのサブフォルダーを再帰的にコピーするかどうかを指定します。|  
  
## <a name="see-also"></a>参照  
 [Hadoop 接続マネージャー](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [ファイル接続マネージャー](../../integration-services/connection-manager/file-connection-manager.md)  
  
  
