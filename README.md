# oor-lyrics-data

歌詞資料 repo。給 [oor-singing-learning](https://github.com/sherry30219-byte/oor-singing-learning) 網站 runtime 抓取使用。

## 結構

```
.
├── index.json                           # 總索引（所有專輯 + 歌曲清單）
└── albums/
    └── <NNN-album-slug>/
        ├── cover.jpg                    # 專輯封面（選填）
        └── songs/
            └── <NN-song-slug>.json      # 一首歌一個檔，含全部語言
```

## index.json

```json
{
  "version": 1,
  "albums": [
    {
      "slug": "001-luxury-disease",
      "title": "Luxury Disease",
      "titleZh": "奢華病",
      "artist": "ONE OK ROCK",
      "year": 2022,
      "cover": "albums/001-luxury-disease/cover.jpg",
      "songs": [
        {
          "slug": "01-save-yourself",
          "title": "Save Yourself",
          "titleZh": "拯救自己",
          "youtubeId": "9ScZ7ZQ4l0Q",
          "duration": 240,
          "file": "albums/001-luxury-disease/songs/01-save-yourself.json"
        }
      ]
    }
  ]
}
```

## 單首歌 JSON

`time` / `endTime` 單位是秒。`jp` 是 segment 陣列，每段 `t`（文字）+ 選填 `r`（振假名）。

```json
{
  "slug": "01-save-yourself",
  "title": "Save Yourself",
  "youtubeId": "9ScZ7ZQ4l0Q",
  "offset": 0,
  "lines": [
    {
      "time": 8.0,
      "endTime": 13.5,
      "jp": [
        { "t": "今日", "r": "きょう" },
        { "t": "も" },
        { "t": "朝", "r": "あさ" }
      ],
      "zh": "今天也是早上",
      "kuso": "kyo 摸 阿撒",
      "romaji": "kyou mo asa"
    }
  ]
}
```

## 新增歌曲流程

1. 在 `albums/<slug>/songs/` 建新的 `<NN-song-slug>.json`
2. 在 `index.json` 對應 album 的 `songs` 陣列加入引用
3. `git commit && git push`
4. 網站 ≤60s 內會反映新內容（CDN revalidate）
