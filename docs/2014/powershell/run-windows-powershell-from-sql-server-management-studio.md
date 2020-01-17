---
title: SQL Server Management Studio から Windows PowerShell を実行する方法 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c6d71f1158ef73b84e5b04dcc9a1970bfd7dce35
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72783101"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から Windows PowerShell を実行する方法
  Windows PowerShell セッションは、 **の** オブジェクト エクスプローラー [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]から起動できます。 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] は、Windows PowerShell を起動し、`sqlps` モジュールを読み込み、**オブジェクトエクスプローラー**ツリー内の関連付けられたノードにパスコンテキストを設定します。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 **オブジェクト エクスプローラー**でオブジェクトに対して PowerShell の実行を指定すると、 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] PowerShell スナップインの読み込みと登録が完了した Windows PowerShell セッションが [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] によって開始されます。 セッションのパスは、オブジェクト エクスプローラーで右クリックしたオブジェクトの場所にあらかじめ設定されています。 たとえば、オブジェクト エクスプローラーで [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] データベース オブジェクトを右クリックして **[PowerShell の起動]** を選択した場合、Windows PowerShell パスは次のように設定されます。  
  
```
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```  
  
## <a name="to-run-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio から PowerShell を実行するには 
  
1.  **オブジェクト エクスプローラー**を開きます。  
  
2.  作業対象オブジェクトのノードに移動します。  
  
3.  オブジェクトを右クリックし、 **[PowerShell の起動]** を選択します。  
  
## <a name="permissions"></a>Permissions  
 PowerShell を [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]で開いた場合は管理者特権で実行されないため、WMI の呼び出しなどの一部のアクティビティが実行されない場合があります。  
  
## <a name="see-also"></a>「  
 [SQL Server PowerShell](sql-server-powershell.md)  
