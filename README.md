# docker-buck

Set of helpers for build Docker images using [Buck](http://buckbuild.com) build system

# Features

`docker(name,src=[],docker_file='Dockerfile',target_name='container')`
Creates `target_name` target that during a run will gather `docker_file` and set of `src` (you can use `location` macroses there as well) and output Docker images as a result

# Example

`tree .`:
``` bash
├── BUCK
├── config.xml
└── Dockerfile
```

`cat BUCK`:
``` python
include_defs('//public/docker-buck/lib')
docker(name = 'phobos',
       src = ['$(location :release)','config.xml'])
```

`cat Dockerfile`:
```
FROM java:8u66-jre
COPY config.xml app.jar
COPY app.jar app.jar
ENV PORT 8080
CMD java -jar app.jar $PORT
```

# Installation

Take [lib](lib) file and put in a right place inside your repo. Then in your BUCK files reference it as `include_defs('//path/to/lib')`. Alternatively use [.buckconfig includes](https://buckbuild.com/concept/buckconfig.html#buildfile.includes)
