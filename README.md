# 🐾 Spring PetClinic CI/CD Project

A production-style CI/CD pipeline for the Spring PetClinic application using Docker and Jenkins.

---

## 🚀 Project Overview

This project is based on the official Spring PetClinic application and enhanced with:

* ✅ Maven build automation
* ✅ Docker containerization
* ✅ Jenkins CI pipeline
* ✅ Ready for Kubernetes deployment

---

## 🛠️ Tech Stack

* Java 17
* Spring Boot
* Maven
* Docker
* Jenkins

---

## 📦 Project Structure

```
spring-petclinic-cicd/
│
├── src/                # Application source code
├── k8s/                # Kubernetes manifests
├── Dockerfile          # Container build definition
├── Jenkinsfile         # CI pipeline
├── pom.xml             # Maven configuration
├── mvnw                # Maven wrapper
└── README.md
```

---

## ⚙️ Run Locally

### 1. Clone the repository

```
git clone https://github.com/abdelatif2030/spring-petclinic-cicd.git
cd spring-petclinic-cicd
```

---

### 2. Run with Maven

```
./mvnw spring-boot:run
```

---

### 3. Open in browser

```
http://localhost:8080
```

---

## 🐳 Run with Docker

### Build image

```
docker build -t spring-petclinic .
```

### Run container

```
docker run -p 8080:8080 spring-petclinic
```

---

## 🔄 CI Pipeline (Jenkins)

The pipeline includes:

1. Checkout source code
2. Build with Maven
3. Build Docker image
4. Push image to DockerHub

---

## 📤 DockerHub Image

```
abdo1997mohamed2030/spring-petclinic:latest
```

---

## 🧪 Database

By default, the application uses:

* H2 in-memory database

You can switch to:

* MySQL
* PostgreSQL

Using Spring profiles:

```
-Dspring.profiles.active=mysql
```

---

## 🐳 Run Database with Docker

### MySQL

```
docker run -e MYSQL_USER=petclinic \
           -e MYSQL_PASSWORD=petclinic \
           -e MYSQL_ROOT_PASSWORD=root \
           -e MYSQL_DATABASE=petclinic \
           -p 3306:3306 mysql
```

---

## ☸️ Kubernetes (Optional)

Kubernetes manifests are available in:

```
k8s/
```

Deploy using:

```
kubectl apply -f k8s/
```

---

## 📌 Notes

* This project is intended for learning DevOps & CI/CD workflows
* Built on top of the official Spring PetClinic sample

---

## 🏁 Future Improvements

* Helm charts
* Multi-environment deployment (dev/stage/prod)
* Monitoring (Prometheus & Grafana)
* Automated testing stage

---

## 📄 License

This project is based on Spring PetClinic and follows Apache License 2.0.

