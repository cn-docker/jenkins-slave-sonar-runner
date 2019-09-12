# Jenkins Slave Sonar Runner

[![](https://img.shields.io/docker/pulls/jnonino/jenkins-slave-sonar-runner.svg)](https://hub.docker.com/r/jnonino/jenkins-slave-sonar-runner/)
[![](hhttps://img.shields.io/docker/build/jnonino/jenkins-slave-sonar-runner)](https://hub.docker.com/r/jnonino/jenkins-slave-sonar-runner/)
[![](https://img.shields.io/docker/automated/jnonino/jenkins-slave-sonar-runner)](https://hub.docker.com/r/jnonino/jenkins-slave-sonar-runner/)
[![](https://img.shields.io/docker/stars/jnonino/jenkins-slave-sonar-runner)](https://hub.docker.com/r/jnonino/jenkins-slave-sonar-runner/)
[![](https://img.shields.io/github/license/cn-cicd/jenkins-slave-sonar-runner)](https://github.com/cn-cicd/jenkins-slave-sonar-runner)
[![](https://img.shields.io/github/issues/cn-cicd/jenkins-slave-sonar-runner)](https://github.com/cn-cicd/jenkins-slave-sonar-runner)
[![](https://img.shields.io/github/issues-closed/cn-cicd/jenkins-slave-sonar-runner)](https://github.com/cn-cicd/jenkins-slave-sonar-runner)
[![](https://img.shields.io/github/languages/code-size/cn-cicd/jenkins-slave-sonar-runner)](https://github.com/cn-cicd/jenkins-slave-sonar-runner)
[![](https://img.shields.io/github/repo-size/cn-cicd/jenkins-slave-sonar-runner)](https://github.com/cn-cicd/jenkins-slave-sonar-runner)

Jenkins Slave for Sonar Runner. Docker image based on OpenJDK official image.

## Tools Installed ##

- Sonar Runner
- Open Java JDK 8
- Git
- Subversion
- Mercurial
- wget
- curl
- unzip
- OpenSSH
- CA Certificates

## Add certificate to connect to HTTPS repositories

To add custom certificates and root CAs, create a new Dockerfile and import them with the following code.

	FROM jnonino/jenkins-slave-sonar-runner
	LABEL maintainer="Julian Nonino <noninojulian@gmail.com>"

	# Trust Root CA
	COPY Root_CA.crt /tmp
	RUN keytool -importcert -alias Root_CA -keystore ${JAVA_HOME}/jre/lib/security/cacerts -storepass changeit -file /tmp/Root_CA.crt -noprompt && \
		cp /tmp/Root_CA.crt /usr/local/share/ca-certificates/ && \
		chmod 644 /usr/local/share/ca-certificates/Root_CA.crt && \
		update-ca-certificates

	CMD ["/bin/bash"]
