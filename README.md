# 🧑‍💼 Employee Management System (EMS)

A backend REST API built with Spring Boot to manage employees, departments, and salaries. Designed for DevOps pipeline integration and production-grade deployment.

---

## 🚀 Features

### 👨‍💻 Developer Side
- **Employee CRUD**: Add, update, delete, and retrieve employees
- **Department CRUD**: Add/update departments and link employees
- **Search & Filter**:
  - Search employees by department
  - Filter employees by salary threshold

### 🔗 REST Endpoints
- `GET /employees`
- `POST /employees`
- `PUT /employees/{id}`
- `DELETE /employees/{id}`
- `GET /departments`
- `GET /employees/search?department=IT`
- `GET /employees/filter?minSalary=50000`

---

## 🧰 Tech Stack

| Layer        | Tool/Tech             |
|--------------|-----------------------|
| Backend      | Spring Boot (2.x/3.x) |
| DB Access    | Spring Data JPA       |
| Database     | H2 (embedded)         |
| Build Tool   | Maven                 |
| Testing      | JUnit + Mockito       |
| Container    | Docker                |
| CI/CD        | Jenkins               |
| Code Quality | SonarQube             |
| Artifact Repo| Nexus OSS             |
| Security     | Trivy (image scanner) |
| Deployment   | Kubernetes (Minikube) |

---

## 🛠️ DevOps Resources

### 📁 Project Root
- `Dockerfile` → Containerize Spring Boot app
- `Jenkinsfile` → CI/CD pipeline stages
- `sonar-project.properties` → SonarQube config
- `README.md` → Project documentation

### 📁 k8s/
- `deployment.yaml` → K8s deployment spec
- `service.yaml` → NodePort service
- `configmap.yaml` → Externalized configs (optional)

---

## ⚙️ CI/CD Pipeline Overview

1. **Build**: Maven compiles and packages the app
2. **SonarQube Scan**: Code quality analysis
3. **Docker Build**: Containerize the app
4. **Trivy Scan**: Security scan of Docker image
5. **Publish to Nexus**: Upload JAR artifact
6. **Deploy to K8s**: Apply manifests via `kubectl`

---

## 📦 How to Run Locally

```bash
./mvnw clean package
java -jar target/employee-management-system.jar

🧪 How to Run in Docker

docker build -t employee-management-system .
docker run -p 8080:8080 employee-management-system


☸️ How to Deploy to Kubernetes

kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
