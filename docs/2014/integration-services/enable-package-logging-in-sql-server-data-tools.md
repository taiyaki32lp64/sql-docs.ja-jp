---
title: パッケージの SQL Server データ ツールにログ記録を有効にする |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- logs [Integration Services], enabling
ms.assetid: b69a8593-5bb0-4f04-87d2-f8e7bd7eb4fc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8ef64ee84a90a74d2206fa8cc766e45b1a691566
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/15/2019
ms.locfileid: "66059282"
---
# <a name="enable-package-logging-in-sql-server-data-tools"></a>SQL Server Data Tools でパッケージのログ記録を有効にする
  この手順では、パッケージにログを追加し、パッケージ レベルのログ記録を構成し、ログ構成を XML ファイルに保存する方法について説明します。 ログはパッケージ レベルでのみ追加できますが、パッケージに含まれるコンテナーでのログを有効にするためにパッケージでログ記録を実行する必要はありません。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] サーバーに配置した場合、パッケージ実行に対して設定したログ記録レベルは、[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] を使用して構成したパッケージのログ記録レベルをオーバーライドします。  
  
 既定では、パッケージに含まれるコンテナーは、親コンテナーと同じログ構成を使用します。 それぞれのコンテナーのログ オプションの設定については、「 [保存されている構成ファイルを使用してログ記録を構成する](../../2014/integration-services/configure-logging-by-using-a-saved-configuration-file.md)」をご覧ください。  
  
### <a name="to-enable-logging-in-a-package"></a>パッケージ内でのログ記録を有効にするには  
  
1.  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]で、目的のパッケージが含まれている [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] プロジェクトを開きます。  
  
2.  次に、 **[SSIS]** メニューの **[ログ記録]** をクリックします。  
  
3.  **[プロバイダーの種類]** 一覧からログ プロバイダーを選択し、 **[追加]** をクリックします。  
  
4.  **[構成]** 列で、接続マネージャーを選択するか、または **[\<新しい接続>]** をクリックしてこのログ プロバイダーに適した種類の接続マネージャーを新しく作成します。 選択したプロバイダーに応じて、次のいずれかの接続マネージャーを使用します。  
  
    -   テキスト ファイル用には、ファイル接続マネージャーを使用します。 詳細については、「 [File Connection Manager](connection-manager/file-connection-manager.md)」(ファイル接続マネージャー) をご覧ください。  
  
    -   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]用には、ファイル接続マネージャーを使用します。  
  
    -   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]用には、OLE DB 接続マネージャーを使用します。 詳細については、「 [OLE DB 接続マネージャー](connection-manager/ole-db-connection-manager.md)」をご覧ください。  
  
    -   Windows イベント ログ用には何も指定しません。 [!INCLUDE[ssIS](../includes/ssis-md.md)] によってログが自動的に作成されます。  
  
    -   XML ファイル用には、ファイル接続マネージャーを使用します。  
  
5.  パッケージで使用するそれぞれのログについて、手順 3. ～ 4. を繰り返します。  
  
    > [!NOTE]  
    >  パッケージでは、それぞれの種類で複数のログを使用できます。  
  
6.  必要に応じて、パッケージレベルのチェック ボックスをオンにします。次に、パッケージレベルのログ記録で使用するログを選択し、 **[詳細]** タブをクリックします。  
  
7.  **[詳細]** タブで、 **[イベント]** をオンにしてすべてのログ エントリのログを記録することを指定するか、または **[イベント]** をオフにしてイベントを個別に選択します。  
  
8.  必要に応じて、 **[詳細設定]** をクリックし、ログに記録する情報を指定します。  
  
    > [!NOTE]  
    >  既定では、すべての情報がログに記録されます。  
  
9. **[詳細]** タブで、 **[保存]** をクリックします。 **[名前を付けて保存]** ダイアログ ボックスが表示されます。 ログ構成を保存するフォルダーに移動し、新しいログ構成のファイル名を入力し、 **[保存]** をクリックします。  
  
10. [**OK**] をクリックします。  
  
11. 更新したパッケージを保存するには、 **[ファイル]** メニューの **[選択されたファイルを上書き保存]** をクリックします。  
  
## <a name="see-also"></a>参照  
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)   
 [Integration Services &#40;SSIS&#41; のログ記録](performance/integration-services-ssis-logging.md)  
  
  
