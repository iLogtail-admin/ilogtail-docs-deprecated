# 代码风格

iLogtail C++使用基于Google代码规范的风格，详细格式约束见[.clang-format](https://github.com/alibaba/ilogtail/blob/main/.clang-format)。Go使用Go标准风格。

## 格式化C++代码
使用VSCode的Clang-Format (by xaver)插件。

或使用命令行进行格式化
```bash
find core/ -type f -iname '*.h' -o -iname '*.cpp' | xargs clang-format -i
```

## 格式化Go代码
使用VSCode的Go (by Go Team at Google)插件。

或使用命令行进行格式化
```bash
find ./ -type f -iname '*.go' -not -iname '*.pb.go' | grep -E -v '/vendor|external/' | xargs gofmt -w
```