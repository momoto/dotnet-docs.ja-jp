---
title: コマンドラインツールF#を使って作業を開始する
description: 任意のオペレーティングシステム (Windows、macOs、またはF# Linux) で .NET Core CLI を使用することにより、シンプルなマルチプロジェクトソリューションを構築する方法について説明します。
ms.date: 03/26/2018
ms.openlocfilehash: f9177e653273e5a2191407c4fb22343ded11fece
ms.sourcegitcommit: a4b10e1f2a8bb4e8ff902630855474a0c4f1b37a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/19/2019
ms.locfileid: "71117924"
---
# <a name="get-started-with-f-with-the-net-core-cli"></a>.NET Core CLI のF#使用を開始する

この記事では、.NET Core CLI を使用しF#て、任意のオペレーティングシステム (Windows、macOS、または Linux) でを開始する方法について説明します。 コンソールアプリケーションによって呼び出されるクラスライブラリを使用して、複数のプロジェクトから成るソリューションを構築します。

## <a name="prerequisites"></a>必須コンポーネント

まず、最新の[.NET Core SDK](https://dotnet.microsoft.com/download)をインストールする必要があります。

この記事では、コマンドラインの使用方法を理解し、適切なテキストエディターを使用することを前提としています。 まだ使用していない場合は、のF#テキストエディターとして [Visual Studio Code](get-started-vscode.md) が最適なオプションです。

## <a name="build-a-simple-multi-project-solution"></a>単純な複数プロジェクトソリューションの構築

コマンドプロンプト/ターミナルを開き、 [dotnet new](../../core/tools/dotnet-new.md)コマンドを使用して、という名前`FSNetCore`の新しいソリューションファイルを作成します。

```dotnetcli
dotnet new sln -o FSNetCore
```

前のコマンドを実行すると、次のディレクトリ構造が生成されます。

```console
FSNetCore
    ├── FSNetCore.sln
```

### <a name="write-a-class-library"></a>クラスライブラリを記述する

ディレクトリを*Fsnetcore*に変更します。

コマンドを`dotnet new`使用して、"ライブラリ" という名前の**src**フォルダーにクラスライブラリプロジェクトを作成します。

```dotnetcli
dotnet new classlib -lang F# -o src/Library
```

前のコマンドを実行すると、次のディレクトリ構造が生成されます。

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

の`Library.fs`内容を次のコードに置き換えます。

```fsharp
module Library

open Newtonsoft.Json

let getJsonNetJson value =
    sprintf "I used to be %s but now I'm %s thanks to JSON.NET!" value (JsonConvert.SerializeObject(value))
```

ライブラリプロジェクトに Newtonsoft. Json パッケージを追加します。

```dotnetcli
dotnet add src/Library/Library.fsproj package Newtonsoft.Json
```

[Dotnet sln add](../../core/tools/dotnet-sln.md)コマンドを`FSNetCore`使用して、ソリューションにプロジェクトを追加します。`Library`

```dotnetcli
dotnet sln add src/Library/Library.fsproj
```

を`dotnet build`実行してプロジェクトをビルドします。 未解決の依存関係は、ビルド時に復元されます。

### <a name="write-a-console-application-that-consumes-the-class-library"></a>クラスライブラリを使用するコンソールアプリケーションを作成する

コマンドを`dotnet new`使用して、App という名前の**src**フォルダーにコンソールアプリケーションを作成します。

```dotnetcli
dotnet new console -lang F# -o src/App
```

前のコマンドを実行すると、次のディレクトリ構造が生成されます。

```console
└── FSNetCore
    ├── FSNetCore.sln
    └── src
        ├── App
        │   ├── App.fsproj
        │   ├── Program.fs
        └── Library
            ├── Library.fs
            └── Library.fsproj
```

`Program.fs`ファイルの内容を次のコードに置き換えます。

```fsharp
open System
open Library

[<EntryPoint>]
let main argv =
    printfn "Nice command-line arguments! Here's what JSON.NET has to say about them:"

    argv
    |> Array.map getJsonNetJson
    |> Array.iter (printfn "%s")

    0 // return an integer exit code
```

[Dotnet add reference](../../core/tools/dotnet-add-reference.md)を使用`Library`して、プロジェクトへの参照を追加します。

```dotnetcli
dotnet add src/App/App.fsproj reference src/Library/Library.fsproj
```

次の`FSNetCore` `App` コマンドを使用して、`dotnet sln add`ソリューションにプロジェクトを追加します。

```dotnetcli
dotnet sln add src/App/App.fsproj
```

NuGet の依存関係を`dotnet restore`復元し`dotnet build` 、を実行してプロジェクトをビルドします。

`src/App`コンソールプロジェクトにディレクトリを変更し、引数とし`Hello World`てを渡してプロジェクトを実行します。

```console
cd src/App
dotnet run Hello World
```

次の結果が表示されます。

```console
Nice command-line arguments! Here's what JSON.NET has to say about them:

I used to be Hello but now I'm ""Hello"" thanks to JSON.NET!
I used to be World but now I'm ""World"" thanks to JSON.NET!
```

## <a name="next-steps"></a>次の手順

次に、さまざまなF#機能の詳細については、「」[のF#ツアー](../tour.md)をご覧ください。
