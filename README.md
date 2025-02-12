# 字幕翻译工具 (Subtitle Translator)

## 简介

这是一个基于 Python 的异步字幕翻译工具，旨在帮助用户将字幕文件从一种语言翻译成另一种语言。该工具支持批量翻译、上下文翻译、翻译质量评估等功能，并提供了缓存机制以提高翻译效率。

## 功能特性

- **批量翻译**：支持将字幕文件分块翻译，提高翻译效率。
- **上下文翻译**：在翻译时包含上下文信息，提高翻译的准确性。
- **翻译质量评估**：使用 LLM（如 ChatGPT）对翻译结果进行质量评估，并提供修改建议。
- **缓存机制**：支持翻译结果的缓存，避免重复翻译相同内容。
- **标点处理**：支持自动去除字幕末尾的标点符号（可选）。
- **并发控制**：支持控制并发翻译任务的数量，避免资源耗尽。

## 安装

### 依赖

- Python 3.7 或更高版本
- `asyncio`、`re`、`pathlib`、`subprocess`、`logging` 等标准库
- `guru` [命令行工具](https://github.com/shafreeck/guru)（用于与 LLM 交互）

### 安装步骤

1. 克隆或下载本仓库到本地。
2. 确保已安装 Python 3.7 或更高版本。
3. 安装依赖：
   ```bash
   pip install -r requirements.txt
   ```
4. 安装 `guru` [命令行工具](https://github.com/shafreeck/guru)（具体安装方法请参考 `guru` 的官方文档）。

## 使用方法

### 命令行参数

```bash
python subtitle_translator.py <input_file> <output_file> [options]
```

- `input_file`: 输入字幕文件路径（支持 `.srt` 格式）。
- `output_file`: 输出字幕文件路径。
- `--chunk-size`: 每次翻译的字幕数量（默认：30）。
- `--max-concurrent`: 最大并发数（默认：10）。
- `--context-size`: 翻译时包含的上下文字幕数量（默认：0）。
- `--split-retry`: 每 N 次重试后拆分任务（默认：1）。
- `--keep-punctuation`: 保留字幕末尾的标点符号（默认会去除）。

### 示例

```bash
python subtitle_translator.py input.srt output.srt --chunk-size 20 --max-concurrent 5 --context-size 3
```

### 输出

翻译完成后，结果将保存到指定的输出文件中。程序会实时显示翻译进度和质量评估结果。

## 配置文件

该工具支持通过命令行参数进行配置，无需额外的配置文件。

## 注意事项

1. **翻译质量**：翻译质量依赖于所使用的 LLM（如 ChatGPT）的性能。建议在使用前对翻译结果进行人工检查。
2. **缓存机制**：翻译结果会被缓存到 `.translate_cache` 目录中，避免重复翻译相同内容。如果需要重新翻译，可以手动删除缓存文件。
3. **并发控制**：根据系统资源情况，合理设置 `--max-concurrent` 参数，避免资源耗尽。

## 常见问题

### 1. 翻译结果不符合预期

- **原因**：可能是由于上下文信息不足或 LLM 的翻译质量不稳定。
- **解决方案**：尝试增加 `--context-size` 参数的值，或者手动调整翻译结果。

### 2. 翻译速度慢

- **原因**：可能是由于并发数设置过低或网络延迟。
- **解决方案**：适当增加 `--max-concurrent` 参数的值，或者检查网络连接。

### 3. 缓存文件过大

- **原因**：长时间使用后，缓存文件可能会占用较多磁盘空间。
- **解决方案**：定期清理 `.translate_cache` 目录中的缓存文件。

## 贡献

欢迎提交 Issue 或 Pull Request 来改进本工具。

## 许可证

本项目采用 MIT 许可证。详情请参阅 [LICENSE](LICENSE) 文件。

---

**注意**：本工具依赖于第三方 LLM 服务（如 ChatGPT），使用时请遵守相关服务的使用条款和隐私政策。
