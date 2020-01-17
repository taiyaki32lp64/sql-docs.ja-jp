---
title: SqlClient による LocalDB のサポート
description: LocalDB データベースの SqlClient サポートについて説明します。
ms.date: 08/15/2019
ms.assetid: cf796898-5575-46f2-ae6e-21e5aa8c4123
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 14cbe4ccf227c9462d2a2dc19fb42d913ca7bc5a
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451971"
---
# <a name="sqlclient-support-for-localdb"></a>SqlClient による LocalDB のサポート

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET をダウンロードする](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server コード名 Denali から、LocalDB と呼ばれる軽量バージョンの SQL Server を使用できるようになります。 このトピックでは、LocalDB データベースに接続する方法について説明します。  
  
## <a name="remarks"></a>Remarks  
LocalDB のインストール方法や LocalDB インスタンスの構成方法など、LocalDB の詳細については、SQL Server オンライン ブックを参照してください。  
  
LocalDB でできることの概要を次に示します。  
  
- Sqllocaldb または app.config ファイルを使用して LocalDB インスタンスを作成し、開始します。  
  
- sqlcmd.exe を使用し、LocalDB インスタンスにデータベースを追加し、変更します。 たとえば、`sqlcmd -S (localdb)\myinst` のようになります。  
  
- LocalDB インスタンスにデータベースを追加するには、`AttachDBFilename` 接続文字列キーワードを使用します。 `AttachDBFilename` を使用するときに、`Database` 接続文字列キーワードを使用してデータベース名を指定しなかった場合、データベースはアプリケーションの終了時に LocalDB インスタンスから削除されます。  
  
- 接続文字列では、次のように LocalDB インスタンスを指定します。 たとえば、インスタンス名が `myInstance` の場合、接続文字列は次のようになります。  
  
```console
server=(localdb)\\myInstance  
```  
  
LocalDB データベースに接続する場合、`User Instance=True` は許可されません。  
  
LocalDB は [Microsoft SQL Server 2012 Feature Pack](https://www.microsoft.com/download/en/details.aspx?id=29065) からダウンロードできます。 sqlcmd.exe を使用し、LocalDB インスタンスのデータを変更する場合、SQL Server 2012 の sqlcmd が表になります。これは SQL Server 2012 Feature Pack からも入手できます。  
  
## <a name="programmatically-create-a-named-instance"></a>プログラムによって名前付きインスタンスを作成する  
アプリケーションでは、名前付きインスタンスを作成し、次のようにデータベースを指定できます。  
  
- App.config ファイルに作成する LocalDB インスタンスを次のように指定します。  インスタンスのバージョン番号は、LocalDB インストールのバージョン番号と同じである必要があります。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <configSections>  
        <section  
        name="system.data.localdb"  
        type="System.Data.LocalDBConfigurationSection,System.Data,Version=4.0.0.0,Culture=neutral,PublicKeyToken=b77a5c561934e089"/>  
      </configSections>  
      <system.data.localdb>  
        <localdbinstances>  
          <add name="myInstance" version="11.0" />  
        </localdbinstances>  
      </system.data.localdb>  
    </configuration>  
    ```  
  
- `server` 接続文字列キーワードを使用して、インスタンスの名前を指定します。  `server` 接続文字列キーワードで指定されたインスタンス名は app.config ファイルで指定された名前と一致する必要があります。  
  
- を指定するには、`AttachDBFilename` 接続文字列キーワードを使用します。MDF ファイル。  
  
## <a name="next-steps"></a>次の手順
- [SQL Server の機能と ADO.NET](sql-server-features-adonet.md)
