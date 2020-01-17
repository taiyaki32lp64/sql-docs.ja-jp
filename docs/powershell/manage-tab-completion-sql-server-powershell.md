---
title: タブ補完の管理 (SQL Server PowerShell) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.openlocfilehash: db8338f832d27fb5362cb44d3b4cf82212472957
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67912238"
---
# <a name="manage-tab-completion-sql-server-powershell"></a>タブ補完の管理 (SQL Server PowerShell)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell スナップインには、Windows PowerShell のタブ補完を制御するための 3 つの変数 ( **$SqlServerMaximumTabCompletion**、 **$SqlServerMaximumChildItems**、 **$SqlServerIncludeSystemObjects**) が追加されました。 入力された文字列で名前が始まるアイテムの一覧を返すタブ補完によって、入力の手間を削減することができます。  

> [!NOTE]
> SQL Server PowerShell モジュールには **SqlServer** と **SQLPS** の 2 つがあります。 **SQLPS** モジュールは (後方互換性のため) SQL Server のインストールに含まれていますが、今後更新されることはありません。 最新の PowerShell モジュールは **SqlServer** モジュールです。 **SqlServer** モジュールには **SQLPS** のコマンドレットの更新バージョンだけでなく、最新の SQL 機能をサポートする新しいコマンドレットも含まれています。  
> SQL Server Management Studio (SSMS) には前のバージョンの **SqlServer** が含まれて*いました*が、SSMS の 16.x バージョンのみです。 PowerShell を SSMS 17.0 以降で使用するには、**SqlServer** モジュールを PowerShell ギャラリーからインストールする必要があります。
> **SqlServer** モジュールをインストールする場合は、「[SQL Server PowerShell のインストール](download-sql-server-ps-module.md)」を参照してください。
  
Windows PowerShell のタブ補完機能では、パスやコマンドレット名の一部を入力して Tab キーを押すと、既に入力した部分に一致する名前のアイテムの一覧を取得できます。 名前の残りの部分を入力しなくても、その一覧からアイテムを選択できます。  
  
多数のオブジェクトを含むデータベースで作業する場合、タブ補完の一覧が大きくなることがあります。 また、ビューなどの一部の種類の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] オブジェクトには、多数のシステム オブジェクトが含まれます。  
  
[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] スナップインでは、タブ補完および **Get-ChildItem**で表示される情報の量を制御するために使用できる 3 つのシステム変数が導入されています。  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 タブ補完の一覧に含めるオブジェクトの最大数を指定します。 *n* を超える数のオブジェクトが含まれるパス ノードで Tab キーを押した場合、タブ補完の一覧が *n*件までで切り捨てられます。 *n* は整数です。 既定の設定は 0 で、これは一覧表示されるオブジェクトの数に制限がないことを示します。  
  
 **$SqlServerMaximumChildItems =** *n*  
 **Get-ChildItem**で表示されるオブジェクトの最大数を指定します。 **n** を超える数のオブジェクトが含まれるパス ノードで *Get-ChildItem* を実行した場合、一覧が *n*件までで切り捨てられます。 *n* は整数です。 既定の設定は 0 で、これは一覧表示されるオブジェクトの数に制限がないことを示します。  
  
 **$SqlServerIncludeSystemObjects =** { **$True** |  **$False** }  
 **$True**の場合、タブ補完と **Get-ChildItem**でシステム オブジェクトが表示されます。 **$False**の場合、システム オブジェクトは表示されません。 既定の設定は **$False**です。  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>SQL Server のタブ補完変数の設定  
 既定値から変更する場合は、その対象となるすべての変数について、新しい値を設定する必要があります。  
  
### <a name="example-powershell"></a>例 (PowerShell)  
 次の例では、3 つすべての変数を設定し、設定を一覧表示します。  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
