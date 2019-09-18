# [SobaScript.Z.Ext](https://github.com/3F/SobaScript.Z.Ext)

Extended Core components for SobaScript. Extensible Modular Scripting Programming Language.

**-- #SobaScript**

https://github.com/3F/SobaScript

[![Build status](https://ci.appveyor.com/api/projects/status/7q5gin883508elb7/branch/master?svg=true)](https://ci.appveyor.com/project/3Fs/sobascript-z-ext/branch/master)
[![release-src](https://img.shields.io/github/release/3F/SobaScript.Z.Ext.svg)](https://github.com/3F/SobaScript.Z.Ext/releases/latest)
[![License](https://img.shields.io/badge/License-MIT-74A5C2.svg)](https://github.com/3F/SobaScript.Z.Ext/blob/master/License.txt)
[![NuGet package](https://img.shields.io/nuget/v/SobaScript.Z.Ext.svg)](https://www.nuget.org/packages/SobaScript.Z.Ext/)
[![Tests](https://img.shields.io/appveyor/tests/3Fs/sobascript-z-ext/master.svg)](https://ci.appveyor.com/project/3Fs/sobascript-z-ext/build/tests)

[![Build history](https://buildstats.info/appveyor/chart/3Fs/sobascript-z-ext?buildCount=20&showStats=true)](https://ci.appveyor.com/project/3Fs/sobascript-z-ext/history)

## License

Licensed under the [MIT License](https://github.com/3F/SobaScript.Z.Ext/blob/master/License.txt)

```
Copyright (c) 2014-2019  Denis Kuzmin < x-3F@outlook.com > GitHub/3F
```

[ [ ☕ Donate ](https://3F.github.com/Donation/) ]

SobaScript.Z.Ext contributors: https://github.com/3F/SobaScript.Z.Ext/graphs/contributors

## Provides at least the following

### SevenZipComponent

```clojure
#[7z pack.files({"IntelOCL.log", "IntelChipset.log"}, "ilog.7z")]
#[7z pack.files({"IntelAMT.log"}, "P:\s01\log.xml"}, "D:\output.zip", Zip, Deflate, 2)]
#[7z pack.files(
    {
        "bin\gpp.exe", 
        "bin\lib\*.dll"
    },
    "gpp.7z", 
    {"bin\lib\stub.dll"}, 
    SevenZip, Lzma2, 4
)]
```

```clojure
#[7z pack.directory("bin", "release.zip")]
#[7z pack.directory("D:\log", "log.7z", SevenZip, Lzma2, 4)]
```

```clojure
#[( !#[7z check("arch.tar.xz")] ){
    #[Build cancel = true]
}]

#[var arch = #[7z check("arch.tar.xz", "pass-123")]]
```

```clojure
#[7z unpack("release.7z", true)]
#[7z unpack("xscale.zip", "D:\app\xscale", false, "pass-123")]
```

### NuGetComponent

Through [GetNuTool](https://github.com/3F/GetNuTool).

```clojure
#[NuGet gnt.raw("/p:ngpackages=\"7z.Libs/19.0.1;vsSBE.CI.MSBuild/1.6.12011:../packages/CI.MSBuild\"")]
```

```clojure
#[NuGet gnt.raw("/t:pack /p:ngin=\"D:\tmp\7z.Libs\" /p:ngout=\"newdir/\"")]
```

### FileComponent

I/O local and remote operations.

```clojure
#[File replace.Regex("source.csproj", "<Version>[0-9.]+</Version>", "<Version>$(version)</Version>")]
#[File replace.Regex("file.log", "(\d+)", "~$1~")]
```

```clojure
#[( #[IO exists.directory("D:\tmp\log")] ){
   ...
}]
```

```clojure
#[IO copy.file("bin\release.7z", "$(out)dep\release.7z", true)]
#[IO copy.file("D:\inc\*.h", "$(SolutionDir)inc/", false, {"ui.core.h", "http.h"})]
#[File appendLine("in.log"): mixed data]
```

```clojure
#[IO copy.file({
                    "bin\client.zip", 
                    "bin\server\*.*"
               }, 
               "$(plugin)\beta", 
               true, 
               { 
                    "*debug*",
                    "*.pdb"
               })]
```

```clojure
#[IO copy.directory("bin", "$(out)dep/mixed", true)]
```

```clojure
#[IO remote.download("ftp://192.168.17.04:2021/dir1/non-api.png", "non-api.png", "usr", "pwd")]
#[IO remote.download("http://example.com", "example.com.html")]
```

### FunctionComponent

mixed functions, such as:

```clojure
#[Func hash.MD5("Hello World!")]
ED076287532E86365E841E92BFC50D8C
```


```clojure
#[Func hash.SHA1("Hello World!")]
2EF7BDE608CE5404E97D5F042F95F89F1C232871
```