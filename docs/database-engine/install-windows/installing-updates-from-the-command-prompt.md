---
title: コマンド プロンプトからの更新プログラムのインストール | Microsoft Docs
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: bc98ba2b-aae9-4d01-aa85-d4c36428cb0b
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 933d8ae26522800326c88a8ba28dbd99c5688fc2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990914"
---
# <a name="installing-updates-from-the-command-prompt"></a>コマンド プロンプトからの更新プログラムのインストール

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

インストール スクリプトをテストし、必要に応じて変更してください。 
 
## <a name="sample-syntax-for-installation"></a>インストールのサンプル構文 
更新プログラム パッケージの名前はさまざまであり、言語、エディション、およびプロセッサ コンポーネントが含まれる場合があります。 コマンド プロンプトで更新プログラムを適用する際に、<package_name> の部分は実際の更新プログラム パッケージの名前に置き換えてください。 
 
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や管理ツールなどのすべての共有コンポーネントを更新します。InstanceName パラメーターまたは InstanceID パラメーターを使用してインスタンスを指定できます。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の準備済みインスタンスを更新するには、InstanceID パラメーターを指定する必要があります。

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceName=MyInstance
    ```
    内の複数の 
    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /InstanceID=\<Instance ID>. 
    ```

- セットアップでは、メインの製品と使用可能な更新プログラムが同時にインストールされるように、最新の製品の更新プログラムとメインの製品のインストールを統合できます。 製品の更新プログラムを含むようにデータベース エンジン インスタンスのインストールを準備することができます。 

    ```
    setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=PrepareImage /UpdateEnabled=True /UpdateSource=\<path where the update is downloaded> /INSTANCEID=\<Instance ID> /FEATURES=SQLEngine. 
    ```

- [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や管理ツールなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共有コンポーネントのみを更新します。 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch 
    ```

- コンピューター上のすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスと、[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や管理ツールなどのすべての共有コンポーネントを更新します。 

    ```
    <package_name>.exe /qs /IAcceptSQLServerLicenseTerms /Action=Patch /AllInstances. 
    ```

- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] の 1 つのインスタンスと [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や管理ツールなどのすべての共有コンポーネントから更新プログラムを削除します。 

    ```
    <package_name>.exe /qs /Action=RemovePatch /InstanceName=MyInstance. 
    ```

- [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] や管理ツールなどの [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 共有コンポーネントのみから更新プログラムを削除します。 

    ```
    <package_name>.exe /qs /Action=RemovePatch 
    ```

  > [!NOTE] 
  > 更新プログラムのインストーラーによって、共有コンポーネントが常に最上位レベルのインスタンスのバージョンと同じかまたはそれ以上であることが保証されます。 
 
## <a name="supported-parameters"></a>サポートされているパラメーター 
 
> [!IMPORTANT] 
> セキュリティ資格情報は、できるだけ実行時に入力してください。 資格情報をスクリプト ファイルに含める必要がある場合は、不正なアクセスが行われないようにファイルをセキュリティで保護してください。 
 
|スイッチ|[説明]| 
|------------|-----------------| 
|**/?**|自動インストールのコマンド プロンプト ヘルプを表示します。| 
|**/action=Patch または /action=RemovePatch**|インストール動作を指定します: Patch または RemovePatch。| 
|**/allinstances**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを、すべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント (共有、インスタンス非対応) に適用します。| 
|**/instancename=InstanceName***|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを、InstanceName という名前の [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント (共有、インスタンス非対応) に適用します。| 
|**/InstanceID=Inst1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムを、Inst1 という [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] インスタンスとすべての [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] コンポーネント (共有、インスタンス非対応) に適用します。| 
|**/quiet**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 更新プログラムのセットアップを自動モードで実行します。| 
|**/qs**|進行状況 UI ダイアログのみを表示します。| 
|**/UpdateEnabled**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップが製品の更新プログラムを検出し、それらを含める必要があるかどうかを指定します。 有効値は True および False または 1 および 0 です。 既定では、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] セットアップには検出された更新プログラムが含まれます。| 
|**/IAcceptSQLServerLicenseTerms**|自動インストールのために /Q パラメーターまたは /QS パラメーターを指定した場合にのみ必須です。| 
 
 *準備済み [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]インスタンスに更新プログラムを適用するために、このパラメーターを指定することはできません。 代わりに /instanceID パラメーターを指定してください。 
 
## <a name="see-also"></a>参照 
 [SQL Server サービスのインストールの概要](https://msdn.microsoft.com/library/6a9fd19b-2367-4908-b638-363b1e929e1e) 
 
 
