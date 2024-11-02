# SonarQube Installation

An open-source code quality tool for better code.

## Documentation

[SonarQube 10.7 Documentation](https://docs.sonarsource.com/sonarqube/latest/)

## Features

- Code Analysis
- Code Quality Metrics
- Continuous Inspection
- Extensive Rules Set

## Benifits

- Improve code maintainability
- Enhance reliability
- Security assurance

## Installation

### Prerequisite:

    1. Docker must have installed in the machine.

Follow the next steps to see your code quality

### Steps

Pull SonarQube image from docker hub [link](https://hub.docker.com/_/sonarqube/tags)

```bash
docker pull sonarqube
```

Configure Postgresql database in docker

```bash
docker run -d --name sonerqube-db -e POSTGRESQL_USER=sonar -e POSTGRESQL_PASSWORD=sonar -e POSTGRESQL_DB=sonarqube postgres:alpine
```

Run SonarQube

```bash
docker run -d --name sonarqube -p 9000:9000 --link sonarqube-db:db -e SONAR_JDBC_URL=jdbc:postgresql://db:5432/sonarqube -e SONAR_JDBC_USERNAME=sonar -e SONAR_JDBC_PASSWORD=sonar sonarqube
```

`This command sets up the SonarQube container with a link to the PostgreSQL database.
`

Show runnign docker process in terminal

```bash
docker ps
```

Set Sonar Scanner Home ( `Optional` )

```bash
nano ~/.bashrc

export SONAR_SCANNER_HOME=/path/to/sonar-scanner

Add Sonar Scanner to PATH
export PATH=$SONAR_SCANNER_HOME/bin:$PATH
```

Open [http://localhost:9000](localhost:9000) in any browser

- Login with default credential ( user: admin | password: admin )
- Set new password ( use old password as admin )
- Create a local projrect from [http://localhost:9000/projects/create](localhost:9000/projects/create) named `sample`
- Fill project details [http://localhost:9000/projects/create?mode=manual](localhost:9000/projects/create?mode=manual)
- Analyze your project from ( click on Localy from bottom ) [http://localhost:9000/tutorials?id=sample](localhost:9000/tutorials?id=sample)
- Generate your project token from [http://localhost:9000/tutorials?id=sample&selectedTutorial=local](localhost:9000/tutorials?id=sample&selectedTutorial=local)
- Download and unzip the Scanner from [ official documentation of the Scanner](https://docs.sonarsource.com/sonarqube/10.7/analyzing-source-code/scanners/sonarscanner/)

Execude the scanner

```bash
[scanner-bin-directory-path]/sonar-scanner \
    Dsonar.projectKey=sample \
    Dsonar.sources=. \
    Dsonar.host.url=http://localhost:9000 \
    Dsonar.token=[replace with your project token]
```

## Re-run SonarQube Container ( after installation successful & PC restart )

Start the `sonarqube-db` Container

```bash
docker start sonarqube-db
```

Start the `sonarqube` Container: Once `sonarqube-db` is running, you can start the sonarqube container:

```bash
docker start sonarqube
```

Verify that `sonarqube-db` & `sonarqube` is Running: After starting it, confirm it’s running with:

```bash
docker ps
```

