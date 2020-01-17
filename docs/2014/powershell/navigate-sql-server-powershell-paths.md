---
title: SQL Server PowerShell パスの移動 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: d68aca48-d161-45ed-9f4f-14122ed30218
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ce1e3a2088214c222cd2c2e84fc333f4993b7a6b
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797813"
---
# <a name="navigate-sql-server-powershell-paths"></a>SQL Server PowerShell パスの移動
  [!INCLUDE[ssDE](../includes/ssde-md.md)] PowerShell プロバイダーは、ファイル パスと同様の構造で、SQL Server のインスタンス内のオブジェクトのセットを公開します。 Windows PowerShell コマンドレットを使用することで、プロバイダー パスを移動し、カスタム ドライブを作成して、入力するパスを短くすることができます。  
  
## <a name="before-you-begin"></a>作業を開始する準備  
 Windows PowerShell では、コマンドレットを実装して、PowerShell プロバイダーによりサポートされるオブジェクトの階層を表すパス構造を移動できます。 そのパス内のノードへ移動したときに、他のコマンドレットを使用して、現在のオブジェクトの基本的な操作を実行することができます。 コマンドレットは頻繁に使用されるため、短い標準の別名が用意されています。 また、コマンドレットを類似のコマンド プロンプトのコマンドにマップする別名のセットと、UNIX シェル コマンド用の別のセットもあります。  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] プロバイダーは、次の表に示すように、プロバイダーのコマンドレットのサブセットを実装します。  
  
|コマンドレット|標準の別名|コマンドの別名|UNIX シェルの別名|[説明]|  
|------------|---------------------|---------------|----------------------|-----------------|  
|**Get-Location**|**gl**|**pwd**|**pwd**|現在のノードを取得します。|  
|`Set-Location`|**sl**|**cd、chdir**|**cd、chdir**|現在のノードを変更します。|  
|**Get-ChildItem**|**gci**|**dir**|**ls**|現在のノードに格納されているオブジェクトの一覧を表示します。|  
|**Get-Item**|**gi**|||現在のアイテムのプロパティを返します。|  
|**Rename-Item**|**rni**|**rn**|**ren**|オブジェクトの名前を変更します。|  
|**Remove-Item**|**ri**|**del、rd**|**rm、rmdir**|オブジェクトを削除します。|  
  
> [!IMPORTANT]  
>  一部の [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 識別子 (オブジェクト名) には、Windows PowerShell のパス名ではサポートされない文字が含まれている場合があります。 それらの文字を含む名前の使用方法の詳細については、「 [PowerShell での SQL Server 識別子](sql-server-identifiers-in-powershell.md)」を参照してください。  
  
### <a name="sql-server-information-returned-by-get-childitem"></a>Get-childitem によって返される SQL Server 情報  
 **Get-ChildItem** (またはその別名の **dir** および **ls** ) で返される情報は、SQLSERVER: パス内の場所によって異なります。  
  
|パスの場所|Get-ChildItem の結果|  
|-------------------|----------------------------|  
|SQLSERVER:\SQL|ローカル コンピューターの名前を返します。 SMO または WMI を使用して他のコンピューター上の [!INCLUDE[ssDE](../includes/ssde-md.md)] のインスタンスに接続している場合は、それらのコンピューターも一覧表示されます。|  
|SQLSERVER:\SQL\\*ComputerName*|コンピューター上の [!INCLUDE[ssDE](../includes/ssde-md.md)] のインスタンスの一覧。|  
|SQLSERVER:\SQL\\*ComputerName*\\*InstanceName*|インスタンス内の最上位レベルのオブジェクトの種類の一覧 (Endpoints、Certificates、Databases など)。|  
|オブジェクト クラスのノード (Databases など)|その種類のオブジェクトの一覧 (データベースの場合は master、model、AdventureWorks2008R2 など)。|  
|オブジェクト名のノード (AdventureWorks2012 など)|オブジェクト内に格納されているオブジェクトの種類の一覧。 たとえば、データベースの場合はテーブルやビューなどのオブジェクトの種類が一覧表示されます。|  
  
 既定では、 **Get-ChildItem** でシステム オブジェクトは一覧表示されません。 システム オブジェクト (たとえば *sys* スキーマ内のオブジェクト) を表示するには、 **Force** パラメーターを使用します。  
  
### <a name="custom-drives"></a>カスタム ドライブ  
 Windows PowerShell では、"PowerShell ドライブ" と呼ばれる仮想ドライブをユーザーが定義できます。 これらのドライブには、パス ステートメントの開始ノードがマップされます。 これらは、通常、頻繁に入力されるパスを短縮するために使用します。 SQLSERVER: パスは長くなることがあり、長くなるとその分 Windows PowerShell ウィンドウ内の領域が使用され、多くの入力が必要になります。 特定のパス ノードで多くの作業を行う場合は、そのノードにマップされる Windows PowerShell のカスタム ドライブを定義することができます。  
  
## <a name="use-powershell-cmdlet-aliases"></a>PowerShell コマンドレットの別名の使用  
 **コマンドレットの別名の使用**  
  
-   完全なコマンドレット名を入力する代わりに、より短い別名、つまり使い慣れたコマンド プロンプト コマンドに割り当てられた名前を入力します。  
  
### <a name="alias-example-powershell"></a>別名の例 (PowerShell)  
 たとえば、次に示す一連のコマンドレットまたは別名のいずれかを使用して、SQLSERVER:\SQL フォルダーに移動しフォルダーの子アイテムの一覧を要求することによって、使用できる [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] インスタンスの一覧を取得することができます。  
  
```powershell
## Shows using the full cmdet name.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## Shows using canonical aliases.  
sl SQLSERVER:\SQL  
gci  
  
## Shows using command prompt aliases.  
cd SQLSERVER:\SQL  
dir  
  
## Shows using Unix shell aliases.  
cd SQLSERVER:\SQL  
ls  
```  
  
## <a name="use-get-childitem"></a>Get-ChildItem の使用  

### <a name="return-information-by-using-get-childitem"></a>Get-childitem を使用した情報の取得
  
1.  子の一覧を取得する対象のノードに移動します。  
  
2.  Get-childitem を実行して、一覧を取得します。  
  
### <a name="get-childitem-example-powershell"></a>Get-ChildItem の例 (PowerShell)  
 これらの例は、SQL Server プロバイダー パス内の異なるノードについて、Get-Childitem で返される情報を示しています。  
  
```powershell
## Return the current computer and any computer  
## to which you have made a SQL or WMI connection.  
Set-Location SQLSERVER:\SQL  
Get-ChildItem  
  
## List the instances of the Database Engine on the local computer.  
Set-Location SQLSERVER:\SQL\localhost  
Get-ChildItem  
  
## Lists the categories of objects available in the  
## default instance on the local computer.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT  
Get-ChildItem  
  
## Lists the databases from the local default instance.  
## The force parameter is used to include the system databases.  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT\Databases  
Get-ChildItem -force  
```  
  
## <a name="create-a-custom-drive"></a>カスタム ドライブの作成  

### <a name="create-and-use-a-custom-drive"></a>カスタム ドライブの作成と使用
  
1.  `New-PSDrive` を使用して、カスタム ドライブを定義します。 `Root` パラメーターを使用して、カスタム ドライブ名で表されるパスを指定します。  
  
2.  `Set-Location` などのパス移動コマンドレットでカスタム ドライブ名を参照します。  
  
### <a name="custom-drive-example-powershell"></a>カスタム ドライブの例 (PowerShell)  
 この例では、配置された AdventureWorks2012 サンプル データベースのコピーのノードにマップする AWDB という名前の仮想ドライブを作成します。 仮想ドライブを使用して、データベース内のテーブルに移動します。  
  
```powershell
## Create a new virtual drive.  
New-PSDrive -Name AWDB -Root SQLSERVER:\SQL\localhost\DEFAULT\Databases\AdventureWorks2012  
  
## Use AWDB: to navigate to a specific table.  
Set-Location AWDB:\Tables\Purchasing.Vendor  
```  
  
## <a name="see-also"></a>参照  
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell パスの操作](work-with-sql-server-powershell-paths.md)   
 [URN から SQL Server プロバイダー パスへの変換](../database-engine/convert-urns-to-sql-server-provider-paths.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
