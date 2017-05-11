# Docker-JAVA-Analysis, JAVA Static Code Analysis

Docker-JAVA-Analysis is a JAVA Static Code Analysis Tool.

## Depends On

- [Checkstyle](http://checkstyle.sourceforge.net/)
- [PMD](https://github.com/pmd/pmd)
- [FindBugs](http://findbugs.sourceforge.net/)
- [Infer](https://github.com/facebook/infer)

## Install dependency tools
- [whalebrew](https://github.com/bfirsh/whalebrew)

## Getting Started

```bash
$ git clone https://github.com/recruit-sumai/docker-java-analysis.git
$ cd docker-java-analysis
$ cp -r {your project} src/
```

## Source code analyzer
### Checkstyle

```bash
For dokcer

# Building
$ docker build -t checkstyletool ./checkstyle

# Analyzing
$ docker run -it -v "$(pwd)":/workdir checkstyletool -c /google_checks.xml -o ./src/_report/checkstyle.log ./src/{your project src}


# Debugging
$ docker run --rm -v "$(pwd)":/workdir -it --entrypoint=ash checkstyletool
```

```bash
For whalebrew

# install(local docker image)
$ docker build -t checkstyletool ./checkstyle
$ whalebrew install checkstyletool

# Analyzing
$ checkstyle -c /google_checks.xml -o ./src/_report/checkstyle.log ./src/{your project src}
```
* Open Your Editor `src/_report/checkstyle.log`

### PMD

```bash
For dokcer

# Building
$ docker build -t pmdtool ./pmd

# Analyzing
$ docker run -it -v "$(pwd)":/workdir pmdtool -d ./src/{your project src} -f text -R java-basic,java-design > ./src/_report/pmd.log


# Debugging
$ docker run --rm -v "$(pwd)":/workdir -it --entrypoint=ash pmdtool
```

```bash
For whalebrew

## install(local docker image)
$ docker build -t pmdtool ./pmd
$ whalebrew install pmdtool

## Analyzing
$ pmd -d ./src/{your project src} -f text -R java-basic,java-design > ./src/_report/pmd.log
```

* Open Your Editor `src/_report/pmd.log`


## Compiled source code analyzer
### FindBugs

```bash
For dokcer

# Building
$ docker build -t findbugstool ./findbugs

# Analyzing
$ docker run -it -v "$(pwd)":/workdir findbugstool -textui -effort:max -low -html -output ./src/_report/findbugs-result.html ./src/{your project src}/classes

# Debugging
docker run --rm -v "$(pwd)":/workdir -it --entrypoint=ash findbugstool
```

```bash
For whalebrew

# install(local docker image)
$ docker build -t findbugstool ./findbugs
$ whalebrew install findbugstool

# Analyzing
$ find ./src/{your project src}/ -name "*.class" -type f | findbugs  -textui -effort:max -low -html > ./src/_report/findbugs-result.html
```
* Open Your Browser `src/_report/findbugs-result.html`


## Compile and source code analyzer
### Infer

```bash
For dokcer

# Building
$ docker build -t infertool ./infer

# Analyzing
## gradle
$ docker run -it -v "$(pwd)":/workdir -w /workdir/src/{your project} infertool -o ./src/_report/infer-out -- gradle clean build
     Or
## mvn
$ docker run -it -v "$(pwd)":/workdir -w /workdir/src/{your project} infertool -o ./src/_report/infer-out -- mvn compile


## Debugging
docker run --rm -v "$(pwd)":/workdir -it --entrypoint=bash infertool
```

```bash
For whalebrew

## install(local docker image)
$ docker build -t infertool ./infer
$ whalebrew install infertool

## Analyzing
## gradle
$ cd ./src/{your project} 
$ infer -o ../_report/infer-out -- gradle clean build
     Or
## mvn
$ cd ./src/{your project} 
$ infer -o ../_report/infer-out -- mvn compile
```

* Open Your Editor `src/_report/infer-out/bugs.txt`
