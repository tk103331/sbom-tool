## 用户指南


## 工具全局子命令

```shell
Usage:
  sbom-tool [command]

Available Commands:
  artifact    collect artifact information
  assembly    assembly sbom document from document segments
  completion  Generate the autocompletion script for the specified shell
  convert     convert sbom document format
  env         build environment info
  generate    generate sbom document
  help        Help about any command
  info        get tool introduction information
  modify      modify sbom document properties
  package     collect package dependencies
  source      collect source code information
  validate    validate sbom document format

Flags:
  -h, --help               help for sbom-tool
      --log-level string   log level (default "info")
      --log-path string    log output path (default "/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output
  -v, --version            version for sbom-tool

Use "sbom-tool [command] --help" for more information about a command.

```

## 工具子命令
 

### 源代码信息采集
收集源代码信息(包括代码指纹)
```
Usage:
  sbom-tool source [flags]

Examples:
sbom-tool source -m 4 -s /path/to/source -l java -o source.json --output-mode singlefile --ignore-dirs .git

Flags:
  -h, --help                 help for source
      --ignore-dirs string   dirs to ignore, skip all dot dirs, split by comma. sample: node_modules,logs
  -l, --language string      specify language(sample: java,cpp) (default "*")
  -o, --output string        output file (default "source.json")
      --output-mode string   output mode, singlefile or multiplefile (default "singlefile")
  -m, --parallelism int      number of parallelism (default 8)
  -p, --path string          project root path(use source path if empty)
  -s, --src string           project source directory(use project root if empty) (default ".")

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output

```

### 依赖包采集
收集包依赖包信息
```shell
Usage:
  sbom-tool package [flags]

Examples:
sbom-tool package -m 4 -p /path/to/project -c maven,npm -o package.json

Flags:
  -c, --collectors string   enable package collectors (default "*")
  -h, --help                help for package
  -o, --output string       output file(empty for only output to console)
  -m, --parallelism int     number of parallelism (default 8)
  -p, --path string         project root path (default ".")

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output


```
### 制品信息采集
采集制品信息
```shell
Usage:
  sbom-tool artifact [flags]

Examples:
sbom-tool artifact -m 4 -d /path/to/dist -o artifact.json -n app -v 1.0 -u company 

Flags:
  -d, --dist string       distribution dir or artifact file (default ".")
  -x, --extract           extract files(only for a single zip,rpm,deb file)
  -h, --help              help for artifact
  -n, --name string       package name of artifact
  -o, --output string     output file (default "artifact.json")
  -m, --parallelism int   number of parallelism (default 8)
  -u, --supplier string   package supplier of artifact
  -v, --version string    package version of artifact

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output


```
### SBOM文档
生成SBOM文档
```shell
Usage:
  sbom-tool generate [flags]

Examples:
sbom-tool generate -m 4 -p /path/to/project -s /path/to/source -d /path/to/dist  -l java -o sbom.spdx.json -f spdx-json --ignore-dirs .git   -n app -v 1.0 -u company -b https://example.com/sbom/xxx

Flags:
  -c, --collectors string    enable package collectors (default "*")
  -d, --dist string          distribution directory (default "./dist")
  -x, --extract              extract files(only for a single zip,rpm,deb file)
  -f, --format string        sbom document format (default "spdx-json")
  -h, --help                 help for generate
      --ignore-dist string   dirs to ignore for dist, skip all dot dirs, split by comma. sample: node_modules,logs
      --ignore-pkg string    dirs to ignore for package, skip all dot dirs, split by comma. sample: node_modules,logs
      --ignore-src string    dirs to ignore for source, skip all dot dirs, split by comma. sample: node_modules,logs
  -l, --language string      specify language(sample: java,cpp) (default "*")
  -n, --name string          package name of artifact
  -b, --namespace string     document namespace base uri
  -o, --output string        output sbom file
  -m, --parallelism int      number of parallelism (default 8)
  -p, --path string          project root path (default ".")
      --skip string          skip some phases.(one of source|package|artifact)
  -s, --src string           project source directory(use project root if empty) (default ".")
  -u, --supplier string      package supplier of artifact
  -v, --version string       package version of artifact

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output


```
### SBOM文档组装
从文档片段组装SBOM文档
```shell
Usage:
  sbom-tool assembly [flags]

Examples:
sbom-tool assembly -p /path/to/segments -o sbom.spdx.json -f spdx-json

Flags:
  -f, --format string      sbom document format (default "spdx-json")
  -h, --help               help for assembly
  -b, --namespace string   document namespace base uri
  -o, --output string      distribution directory
  -p, --path string        sbom segments dir (default ".")

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output

```
### SBOM文档格式转换
转换SBOM文档格式
```shell
Usage:
  sbom-tool convert [flags]

Examples:
sbom-tool convert -i /path/to/sbom -g xspdx-json -f spdx-json -o sbom.spdx.json

Flags:
  -f, --format string     the sbom document format convert to
  -h, --help              help for convert
  -i, --input string      input sbom document
  -g, --original string   the sbom document format convert from
  -o, --output string     output sbom document

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output



```
 
### SBOM文档格式验证
验证SBOM文档格式
```shell
Usage:
  sbom-tool validate [flags]

Examples:
sbom-tool validate -i /path/to/sbom -f spdx-json -o result.json

Flags:
  -f, --format string   the sbom document format to validate
  -h, --help            help for validate
  -i, --input string    input sbom document
  -o, --output string   output result to file

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output


```

### SBOM文档字段修改
支持部分指定字段的数据修改功能
```shell
Usage:
  sbom-tool modify [flags]

Examples:
sbom-tool modify -i /path/to/sbom -f spdx-json -o sbom.spdx.json

Flags:
      --add-creator stringArray   add creator of document, example: '"Person: Tim (tim@demo.com)"' (for xspdx); add creator of document, example: '"Person: Tim (tim@demo.com)"' (for spdx)
  -f, --format string             the sbom document format modify to
  -h, --help                      help for modify
  -i, --input string              input sbom document
  -o, --output string             output sbom document
      --set-build stringArray     set properties of artifact.build, example: '{"os":"CentOS","arch":"amd64","kernel":"Linux","builder":"","compiler":""}' (for xspdx)

Global Flags:
      --log-level string   log level (default "info")
      --log-path string    log output path (default "~/sbom-tool/sbom-tool.log")
  -q, --quiet              no console output


```

### 获取工具介绍信息
工具介绍信息及支持的编码语言、编译器、SBOM文档格式列表
```shell
Usage:
  sbom-tool info

Examples:
sbom-tool info
```

## 测试

```shell
make test  # 单元测试
make bench # 性能测试
```