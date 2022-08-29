# Simplified GMT Tutorials

- 修改自: [GMT5 Tutorials](https://jimmytseng79.github.io/GMT5_tutorials/)
- 文件產生工具: [MkDocs](https://www.mkdocs.org/)
- 文件使用語法: Markdown (混 HTML 語法)

## 離線產生 HTML 文件

### 需求
- Python3
- [Poetry](https://python-poetry.org/)

### 安裝
```
poetry install
```

### 預覽
```
poetry run mkdocs serve
```

### 產生文件
```bash
poetry run mkdocs build
poetry run python3 -m http.server -d site/  ## 檢視產生出的 HTML 文件
```
