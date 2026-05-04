# cicd-localstack

100% local CI/CD pipeline -> no paid services, no cloud required.

## Stack
```
Service		Role			URL
Gitea		Git server		http://localhost:3000
Jenkins		CI/CD orchestrator	http://localhost:8080
SonarQube 	CECode analysis		http://localhost:9000
Nexus OSS	Artifact repository	http://localhost:8081
```

## Architecture
```
Push -> Gitea -> webhook -> Jenkins
                            |-> Maven build & test
                            |-> SonarQube analysis + Quality Gate
Quality Gate
                            |-> Nexus publish (.war)
                            |-> Docker build & run (deploy)
```

## Quick Start

0. Prerequisites (Linux/Mac): sudo sysctl -w vm.max_map_count=262144
1. Start the stack: docker compose up -d
2. Check all services are healthy: docker compose ps

## Project Steps
```
1. docker-compose.yml with Gitea, Jenkins, SonarQube, Nexus
2. Gitea: organisation, repository, webhook
3. Jenkins: plugins (SonarQube, Nexus, Docker Pipeline)
4. Jenkinsfile: Checkout -> Build -> Test -> SonarQube Scan
5. SonarQube Quality Gate (coverage >70%, 0 critical bugs)
6. Publish .war to Nexus OSS
7. Deploy stage: Docker image build + run
8. Full flow validation: code push-> pipeline auto-triggers
```
## Replaces
```
Cloud/Paid		Local alternative
GitHub			Gitea
GitHub Actions (paid)	Jenkins OSS
SonarCloud		SonarQube CE
Nexus Cloud		Nexus OSS
AWS ECS			Docker local
```
