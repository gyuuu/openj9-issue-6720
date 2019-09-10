FROM gyuuu/maven-openj9:jdk11-20190906-184832
WORKDIR /build
ADD src/ src/
COPY pom.xml .
RUN ls
RUN mvn clean package

#FROM adoptopenjdk/openjdk8-openj9:debian-slim
FROM gyuuu/openj9:jdk11-20190906-184832
WORKDIR /app
COPY --from=0 /build/target/demo-*.jar demo.jar
COPY --from=0 /build/classCache /classCache
ENV PORT 8080
ENV JAVA_OPTS -Xquickstart -Xtune:virtualized
ENTRYPOINT exec java $JAVA_OPTS -XshowSettings:vm -Xshareclasses:cacheDir=/classCache,name=demo,noPersistentDiskSpaceCheck,readonly -Xscmx32m -Dserver.port=${PORT} -Djava.security.egd=file:/dev/./urandom -jar demo.jar
#ENTRYPOINT exec java $JAVA_OPTS -XshowSettings:vm -Xshareclasses:cacheDir=/classCache,readonly,name=demo -Xscmx32m -Dserver.port=${PORT} -Djava.security.egd=file:/dev/./urandom -jar demo.jar

