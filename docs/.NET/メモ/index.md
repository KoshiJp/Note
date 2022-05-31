# .NET / メモ

## ASP.NET Core MVC

### Razorランタイムコンパイルを有効にする

[ASP.NET Core での Razor ファイルのコンパイル | 既存のプロジェクトで実行時コンパイルを有効にする](ASP.NET Core での Razor ファイルのコンパイル)
```cs
public void ConfigureServices(IServiceCollection services)
{
    services.AddRazorPages().AddRazorRuntimeCompilation();
}
```