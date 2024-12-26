FROM maven:3.9.9-eclipse-temurin-21-jammy AS build_image
RUN until git clone https://github.com/hkhcoder/vprofile-project.git; do echo "Retrying"; done && \
	cd vprofile-project && git checkout containers && mvn install


FROM tomcat:10-jdk21
LABEL "project"="Vpofile"
LABEL "Author"="Ammar"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]