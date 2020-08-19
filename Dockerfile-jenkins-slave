FROM jenkins/jnlp-slave:3.27-1
USER root
RUN apt-get update -qq \
    && apt-get install -qqy apt-transport-https ca-certificates curl gnupg2 software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/debian \
   $(lsb_release -cs) \
   stable"
RUN apt-get update  -qq \
    && apt-get install docker-ce=17.12.1~ce-0~debian -y
RUN usermod -aG docker jenkins

RUN mkdir /usr/share/tools

ENV PATH="/usr/share/tools:${PATH}"

RUN wget -q https://services.gradle.org/distributions/gradle-6.5.1-bin.zip
RUN sleep 30
RUN unzip -d /usr/share/tools gradle-6.5.1-bin.zip
ENV PATH="/usr/share/tools/gradle-6.5.1/bin:${PATH}"

RUN curl -O http://mirrors.ibiblio.org/apache/maven/maven-3/3.2.5/binaries/apache-maven-3.2.5-bin.tar.gz
RUN sudo tar xzf apache-maven-3.2.5-bin.tar.gz -C /usr/share/tools
ENV PATH="/usr/share/tools/apache-maven-3.2.5/bin:${PATH}"
COPY settings.xml /usr/share/tools/apache-maven-3.2.5/conf

RUN wget https://download.java.net/java/GA/jdk12.0.2/e482c34c86bd4bf8b56c0b35558996b9/10/GPL/openjdk-12.0.2_linux-x64_bin.tar.gz
RUN mv openjdk-12.0.2_linux-x64_bin.tar.gz /usr/share/tools/
RUN tar -xzvf /usr/share/tools/openjdk-12.0.2_linux-x64_bin.tar.gz -C /usr/share/tools/
RUN echo "JAVA_HOME='/usr/share/tools/jdk-12.0.2'" > /etc/mavenrc
RUN echo "MAVEN_OPTS='-XX:+TieredCompilation -XX:TieredStopAtLevel=1'" >> /etc/mavenrc
