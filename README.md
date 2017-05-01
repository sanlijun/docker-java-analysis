# Docker-JAVA-Analysis, JAVA Static Code Analysis

Docker-JAVA-Analysis is a JAVA Static Code Analysis Tool.

## Depends On

- [Checkstyle](http://checkstyle.sourceforge.net/)
- [PMD](https://github.com/pmd/pmd)
- [FindBugs](http://findbugs.sourceforge.net/)
- [Infer](https://github.com/facebook/infer)

## Getting Started

```bash
$ git clone https://github.com/recruit-sumai/docker-java-analysis.git
$ cd docker-java-analysis
$ cp -r {your project} src/
```

## Source code analyzer
### Checkstyle

```bash
# Building
$ docker build -t checkstyletool ./checkstyle

# Analyzing
$ docker run --rm --volume `pwd`/src:/usr/workdir/src checkstyletool /bin/ash -c 'java -jar ../checkstyle.jar -c /google_checks.xml -o _report/checkstyle.log ./{your project src}'


# Debugging
docker run --rm -it -v `pwd`/src:/usr/workdir/src checkstyletool /bin/ash
```

* Open Your Editor `src/_report/checkstyle.log`

### PMD

```bash
# Building
$ docker build -t pmdtool ./pmd

# Analyzing
$ docker run --rm --volume `pwd`/src:/usr/workdir/src pmdtool /bin/ash -c '../pmd-bin/bin/run.sh pmd -d ./{your project src} -f text -R java-basic,java-design > _report/pmd.log'


# Debugging
docker run --rm -it -v `pwd`/src:/usr/workdir/src pmdtool /bin/ash
```

* Open Your Editor `src/_report/pmd.log`


## Compiled source code analyzer
### FindBugs

```bash
# Building
$ docker build -t findbugstool ./findbugs

# Analyzing
$ docker run --rm --volume `pwd`/src:/usr/workdir/src findbugstool /bin/ash -c 'find ./{your project} -name "*.class" -type f | xargs java -jar ../findbugs/lib/findbugs.jar -textui -effort:max -low -html > _report/findbugs-result.html'


# Debugging
docker run --rm -it -v `pwd`/src:/usr/workdir/src findbugstool /bin/ash
```

* Open Your Browser `src/_report/findbugs-result.html`


## Compile and source code analyzer
### Infer

```bash
# Building
$ docker build -t infertool ./infer

# Analyzing
## gradle
$ docker run --rm --volume `pwd`/src:/usr/workdir/src infertool /bin/bash -c 'cd ./{your project};infer -o /usr/workdir/src/_report/infer-out -- gradle clean build'
     Or
## mvn
$ docker run --rm --volume `pwd`/src:/usr/workdir/src infertool /bin/bash -c 'cd ./{your project};infer -o /usr/workdir/src/_report/infer-out -- mvn compile'


# Debugging
docker run --rm -it -v `pwd`/src:/usr/workdir/src infertool /bin/bash
```

* Open Your Editor `src/_report/infer-out/bugs.txt`
