# DNCefView.WPF

WPF-only repository for embedding Chromium (CEF) in .NET applications via `DNCefView.WPF`.

## Prerequisites

- Windows
- .NET 8 SDK

## Repository Layout

- `src/DNCefView.WPF/`: WPF control library source.
- `demo/DNCefView.WPF.Demo/`: runnable WPF demo.
- `DNCefView.WPF.slnx`: solution entrypoint.

## Run Demo (single command)

```powershell
dotnet run --project demo/DNCefView.WPF.Demo/DNCefView.WPF.Demo.csproj -c Debug
```

`dotnet run` will automatically restore NuGet packages and build before launch. No manual `nuget` command or separate restore step is required.

## Build and Test

```powershell
# smoke
dotnet restore DNCefView.WPF.slnx
# build
dotnet build DNCefView.WPF.slnx -c Debug
# test
dotnet test DNCefView.WPF.slnx -c Debug --no-build
```

## Runtime Verification

```powershell
dotnet run --project demo/DNCefView.WPF.Demo/DNCefView.WPF.Demo.csproj -c Debug
Get-ChildItem demo/DNCefView.WPF.Demo/bin/Debug/net8.0-windows -Recurse -Filter CCefView.dll
```

## Pre-Publish Checklist

```powershell
dotnet restore DNCefView.WPF.slnx
dotnet build DNCefView.WPF.slnx -c Release
dotnet test DNCefView.WPF.slnx -c Release --no-build
dotnet run --project demo/DNCefView.WPF.Demo/DNCefView.WPF.Demo.csproj -c Debug
```

- Confirm `CCefView.dll` is present under `demo/DNCefView.WPF.Demo/bin/<Configuration>/net8.0-windows/runtimes/win-x64/native/`.
- Confirm demo launches on a clean machine with .NET 8 SDK and network access for first restore.

## Notes

- Runtime native dependencies (including `CCefView.dll`) are provided through NuGet runtime assets from `DNCefView` package version `1.0.8`.
- First run requires network access to fetch packages.

## License

See [LICENSE](LICENSE).
