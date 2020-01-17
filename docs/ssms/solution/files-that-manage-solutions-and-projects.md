---
title: ソリューションとプロジェクトを管理するためのファイル | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- projects [SQL Server Management Studio], files
- .ssmssln files
- .ssmsmobileproj files
- .ssmsasproj files
- .ssmssqlproj files
- .sqlsuo files
- files [SQL Server Management Studio], projects
ms.assetid: e19d2859-0b97-4727-ac27-c4c226d86b2f
author: markingmyname
ms.author: maghan
ms.openlocfilehash: fbaa867ae3ab2683507c773c411d965a46cf795b
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/16/2019
ms.locfileid: "68262871"
---
# <a name="files-that-manage-solutions-and-projects"></a>ソリューションとプロジェクトを管理するためのファイル
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
 ここでは、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]固有の種類のファイルについて説明します。 既定では、すべてのソリューションとプロジェクトが \My Documents\SQL Server Management Studio\Projects に作成されます。  


## <a name="management-studio-solution-files"></a>Management Studio のソリューション ファイル  
[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] では、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] や [!INCLUDE[msCoName](../../includes/msconame_md.md)] Visual Studio とは異なる種類のファイルを使用します。 そのため、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のソリューションを [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull_md.md)] や Visual Studio で開くことはできません。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] のソリューション ファイルの場合、ソリューション エクスプローラーを使用して、ファイルを管理するためのグラフィカル インターフェイスを表示できます。  
   
|拡張子|ファイルの種類|[説明]|作成者|  
|-------------|-------------|---------------|--------------|  
|.ssmssln|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ソリューション オブジェクト|環境に対して、 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] のプロジェクト、プロジェクト アイテム、およびソリューションのディスク上の場所に対する参照を提供します。|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
  
## <a name="management-studio-project-files"></a>Management Studio のプロジェクト ファイル  
ソリューションにソリューション ファイル (つまり、ソリューション内のオブジェクトを管理するためのファイル) があるのと同じように、プロジェクトにはプロジェクト ファイルがあります。 プロジェクトのために [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] によって作成されるプロジェクト ファイルの種類は、プロジェクトの作成に使用するテンプレートによって異なります。 次の表に、各プロジェクトで作成されるファイルの種類をまとめます。  
   
|拡張子|プロジェクト テンプレート|  
|-------------|--------------------|  
|.ssmssqlproj|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] スクリプト プロジェクト|  
|.ssmsasproj|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion_md.md)] スクリプト プロジェクト|  
   
## <a name="location-of-solution-level-files"></a>ソリューション レベルのファイルの場所  
既定では、ソリューション レベルのファイルは、そのソリューションで作成された最初のプロジェクトの物理ディレクトリに作成されます。 ソリューションを作成することによってソリューションのディレクトリを指定することも、新しいプロジェクトを作成するときにディレクトリを指定することも可能です。  
 
ソリューション エクスプローラーに表示される論理構造とよく似たディレクトリ構造があれば、プロジェクト ファイルとソリューション ファイルを見つけることや、チーム内の他の開発者と共有することが容易になります。  
   
## <a name="see-also"></a>参照  
[エンコーディングによるファイルの管理](../../ssms/solution/manage-files-with-encoding.md)  
[その他のファイル](../../ssms/solution/miscellaneous-files.md)  
[ソリューション エクスプローラー](../../ssms/solution/solution-explorer.md)  
[ソリューション (SQL Server Management Studio)](../../ssms/solution/solutions-sql-server-management-studio.md)  
[プロジェクト (SQL Server Management Studio)](../../ssms/solution/projects-sql-server-management-studio.md)  
[ソリューション エクスプローラーのソース管理](https://msdn.microsoft.com/library/ms173879.aspx)  
  
