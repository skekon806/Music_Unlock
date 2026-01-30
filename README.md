# 国内流媒体音乐下载管理

## 网易云音乐下载

一月一次领免费会员活动，一月80首下载额度。得到ncm格式，使用[ncmdump](https://github.com/taurusxin/ncmdump)

```bat
ncmdump -d /path/to/VipSongsDownload/-o /path/to/your/music/folder
```

得到解锁格式flac。

## 酷狗音乐下载

合租¥30/年，每月300首下载额度，月末清空剩余额度。得到kgma/kgg格式。

### kgma格式

使用[kugou-kgm-decoder](https://github.com/ghtz08/kugou-kgm-decoder)转换得到mp3格式，并删除原kgma格式文件。实际编码可能为flac可自行重命名。

```bat
:: 先复制到保存音频的文件夹
set "SRC_DIR=/path/to/KugouMusic/"
set "DEST_DIR=/path/to/your/music/folder/"
xcopy "%SRC_DIR%\*.kgma" "%DEST_DIR%\" /Y

kgm-decoder-windows-amd64 "%DEST_DIR%\"
```
### kgg格式

使用[kgg-dec](https://github.com/DHJComical/kgg-dec-mirror)转换，在kgg同目录下得到flac/mp3/ogg格式。

```bat
kgg-dec "%SRC_DIR%\"
:: 移动flac/mp3/ogg音频文件
move "%SRC_DIR%\*.mp3" "%DEST_DIR%\" >nul 2>&1
move "%SRC_DIR%\*.flac" "%DEST_DIR%\" >nul 2>&1
move "%SRC_DIR%\*.ogg" "%DEST_DIR%\" >nul 2>&1
```

## exiftool文件管理
/path/to/your/music/folder
└── Taylor Swift
    ├── evermore 
    │   └── champagne problems.flac
    │   └── closure.flac
    │   └── ...
    └── folklore (deluxe version)
    │   └── august.flac
    │   └── betty.flac
    │   └── ...
```bat
exiftool ^
  -ext flac ^
  -r ^
  "-Directory</path/to/your/music/folder/$Artist/$Album" ^
  "-Filename<$Title.flac" ^
  -overwrite_original ^
  "/path/to/your/music/folder"
pause
```
