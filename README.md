# Netflix Clone — DevSecOps CI/CD Pipeline

A production-grade DevSecOps pipeline that automatically builds, scans, and deploys a Netflix clone application to Kubernetes on AWS.

Live App: http://65.0.27.199:30007

## Architecture

GitHub -> Jenkins -> SonarQube -> OWASP -> Docker -> Trivy -> DockerHub -> Kubernetes
                                                      Prometheus + Grafana monitor everything

## Tech Stack

- CI/CD: Jenkins
- Code Quality: SonarQube
- Dependency Scanning: OWASP Dependency Check
- Containerization: Docker
- Image Security: Trivy
- Container Registry: DockerHub
- Orchestration: Kubernetes (kubeadm)
- Monitoring: Prometheus + Grafana
- Cloud: AWS EC2 (ap-south-1)
- Notifications: Jenkins Email Extension

## Infrastructure

4 AWS EC2 instances (Ubuntu 22.04):
- jenkins-server: Jenkins, SonarQube, Docker, Trivy
- monitoring-server: Prometheus, Grafana, Node Exporter
- k8s-master: Kubernetes control plane
- k8s-worker: Kubernetes worker node

## Pipeline Stages

1. Clean Workspace - fresh build environment every run
2. Checkout from Git - pulls latest code from GitHub
3. SonarQube Analysis - static code analysis for bugs and vulnerabilities
4. Quality Gate - fails pipeline if code quality threshold not met
5. Install Dependencies - npm install
6. OWASP Dependency Check - scans third-party libraries for known CVEs
7. Trivy FS Scan - scans filesystem for vulnerabilities
8. Docker Build and Push - builds image, pushes to DockerHub
9. Trivy Image Scan - scans Docker image for vulnerabilities
10. Deploy to Kubernetes - applies deployment and service manifests
11. Email Notification - sends build result with logs and scan reports

## Monitoring

Prometheus scrapes metrics from all four servers every 15 seconds.
Grafana dashboards: Node Exporter Full (1860), Jenkins Performance and Health (9964)

## Author

Zain Masood
