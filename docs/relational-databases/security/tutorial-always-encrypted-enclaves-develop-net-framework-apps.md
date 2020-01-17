---
title: チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET Framework アプリケーションを開発する | Microsoft Docs
ms.custom: ''
ms.date: 10/15/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.suite: sql
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: tutorial
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: b73d24edb139e36f11e05c854c9d10d885994e18
ms.sourcegitcommit: 312b961cfe3a540d8f304962909cd93d0a9c330b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73595487"
---
# <a name="tutorial-develop-a-net-framework-application-using-always-encrypted-with-secure-enclaves"></a>チュートリアル:セキュリティで保護されたエンクレーブが設定された Always Encrypted を使用して .NET Framework アプリケーションを開発する
[!INCLUDE [tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx-winonly.md)]

このチュートリアルでは、[セキュリティで保護されたエンクレーブが設定された Always Encrypted](encryption/always-encrypted-enclaves.md) に対してサーバー側のセキュリティで保護されたエンクレーブを使用するデータベース クエリを発行する、簡単なアプリケーションを開発する方法について説明します。 

## <a name="prerequisites"></a>Prerequisites
このチュートリアルは、「[チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](./tutorial-getting-started-with-always-encrypted-enclaves.md)」に続くものです。 以下の手順に従う前に、それが完了していることを確認してください。

さらに、Visual Studio (バージョン 2019 を推奨) が必要です。[https://visualstudio.microsoft.com/](https://visualstudio.microsoft.com) からダウンロードできます。 アプリケーション開発用コンピューターでは、.NET Framework 4.7.2 以降が実行されている必要があります。

## <a name="step-1-set-up-your-visual-studio-project"></a>手順 1:Visual Studio プロジェクトを設定する

.NET Framework アプリケーションでセキュリティで保護されたエンクレーブが設定された Always Encrypted を使用するには、.NET Framework 4.7.2 をターゲットにしてアプリケーションを構築し、[Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders) と統合する必要があります。 さらに、列マスター キーを Azure Key Vault に格納する場合は、アプリケーションを [Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider) バージョン 2.2.0 以降と統合する必要があります。 

1. Visual Studio を開きます。

2. 新しい C\# コンソール アプリ (.NET Framework) プロジェクトを作成します。

3. プロジェクトは必ず .NET Framework 4.7.2 以降をターゲットにします。 ソリューション エクスプローラーでプロジェクトを右クリックし、[プロパティ] を選択し、[ターゲット フレームワーク] を [.NET Framework 4.7.2] に設定します。

4. **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders -IncludePrerelease
   ```

5. Azure Key Vault を使用して列マスター キーを格納する場合は、 **[ツール]** (メイン メニュー) > **[NuGet パッケージ マネージャー]**  >  **[パッケージ マネージャー コンソール]** に移動して、次の NuGet パッケージをインストールします。 パッケージ マネージャー コンソールで次のコードを実行します。

   ```powershell
   Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider -IncludePrerelease -Version 2.2.0
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   ```

7. プロジェクトの App.config ファイルを開きます。

8. \<configuration\> セクションを見つけて、\<configsections\> セクションを追加または更新します。

   A. \<configuration\> セクションに \<configSections\> セクションが含まれて**いない**場合は、\<configuration\> のすぐ下に次の内容を追加します。
   
      ```xml
      <configSections>
         <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
      </configSections>
      ```
   B. \<configruation\> セクションに既に \<configSections\> セクションが含まれている場合、\<configSections\> 内に次の行を追加します。

   ```xml
   <section name="SqlColumnEncryptionEnclaveProviders"  type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data,  Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" /\>
   ```

9. configuration セクション内の \<configSections\> の下に次のセクションを追加します。これは構成証明と VBS エンクレーブとの対話に使用されるエンクレーブ プロバイダーに固有のものです。

   ```xml
   <SqlColumnEncryptionEnclaveProviders>
       <providers>
           <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
       </providers>
   </SqlColumnEncryptionEnclaveProviders>
   ```

単純なコンソール アプリケーションの app.config ファイルの完全な例を次に示します。
```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <configSections>
    <section name="SqlColumnEncryptionEnclaveProviders" type="System.Data.SqlClient.SqlColumnEncryptionEnclaveProviderConfigurationSection, System.Data, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />
  </configSections>
  <SqlColumnEncryptionEnclaveProviders>
    <providers>
      <add name="VBS"  type="Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders.HostGuardianServiceEnclaveProvider,  Microsoft.SqlServer.Management.AlwaysEncrypted.EnclaveProviders,    Version=15.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91"/>
    </providers>
  </SqlColumnEncryptionEnclaveProviders>
  <startup> 
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.7.2" />
  </startup>
</configuration>
```
## <a name="step-2-implement-your-application-logic"></a>手順 2:アプリケーションのロジックを実装する
このアプリケーションでは、**ContosoHR** データベース (「[チュートリアル: SSMS を使用したセキュリティで保護されたエンクレーブを持つ Always Encrypted の概要](tutorial-getting-started-with-always-encrypted-enclaves.md)」のもの) に接続し、**SSN** 列に対する `LIKE` 述語と、**Salary** に対する範囲比較が含まれるクエリを実行します。

1. (Visual Studio によって生成された) Program.cs ファイルの内容を、次のコードに置き換えます。 データベース接続文字列を、お使いのサーバー名と、お使いの環境のエンクレーブ構成証明 URL で更新します。 また、データベースの認証設定を更新することもできます。

    ```cs
    using System;
    using System.Data.SqlClient;
    using System.Data;

    namespace ConsoleApp1
    {
        class Program
        {
            static void Main(string[] args)
            {
    
                string connectionString = "Data Source = myserver; Initial Catalog = ContosoHR; Column Encryption Setting = Enabled;Enclave Attestation Url = http://hgs.bastion.local/Attestation; Integrated Security = true";

                using (SqlConnection connection = new SqlConnection(connectionString))
                {
                    connection.Open();

                    SqlCommand cmd = connection.CreateCommand();
                    cmd.CommandText = @"SELECT [SSN], [FirstName], [LastName], [Salary] FROM [dbo].[Employees] WHERE [SSN] LIKE @SSNPattern AND [Salary] > @MinSalary;";

                    SqlParameter paramSSNPattern = cmd.CreateParameter();

                    paramSSNPattern.ParameterName = @"@SSNPattern";
                    paramSSNPattern.DbType = DbType.AnsiStringFixedLength;
                    paramSSNPattern.Direction = ParameterDirection.Input;
                    paramSSNPattern.Value = "%1111";
                    paramSSNPattern.Size = 11;

                    cmd.Parameters.Add(paramSSNPattern);

                    SqlParameter MinSalary = cmd.CreateParameter();

                    MinSalary.ParameterName = @"@MinSalary";
                    MinSalary.DbType = DbType.Currency;
                    MinSalary.Direction = ParameterDirection.Input;
                    MinSalary.Value = 900;

                    cmd.Parameters.Add(MinSalary);
                    cmd.ExecuteNonQuery();
    
                    SqlDataReader reader = cmd.ExecuteReader();
                    while (reader.Read())

                    {
                        Console.WriteLine(reader);
                        Console.WriteLine(reader[0] + ", " + reader[1] + ", " + reader[2] + ", " + reader[3]);
                    }   
                    Console.ReadKey();
                }
            }
        }
    }
    ```
2. アプリケーションをビルドして実行します。  

## <a name="see-also"></a>参照
- [Always Encrypted と .NET Framework Data Provider for SQL Server を使用する](encryption/develop-using-always-encrypted-with-net-framework-data-provider.md)