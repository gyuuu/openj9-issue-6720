#FROM adoptopenjdk/openjdk8-openj9:debian-slim
FROM gyuuu/openj9:jdk8-20190906-184840
WORKDIR /app
ADD target/demo-*.jar demo.jar
ADD classCache /classCache
ENV PORT 8080
ENV JAVA_OPTS -Xquickstart -Xtune:virtualized
#ENTRYPOINT exec java $JAVA_OPTS -XshowSettings:vm -Xshareclasses:cacheDir=/classCache,readonly,name=demo,noPersistentDiskSpaceCheck -Xscmx32m -Dserver.port=${PORT} -Djava.security.egd=file:/dev/./urandom -jar demo.jar
ENTRYPOINT exec java $JAVA_OPTS -XshowSettings:vm -Xshareclasses:cacheDir=/classCache,readonly,name=demo -Xscmx32m -Dserver.port=${PORT} -Djava.security.egd=file:/dev/./urandom -jar demo.jar

