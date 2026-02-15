# PROJECT_CONTEXT.md

## Project Overview

This project is a hands-on DevSecOps implementation built on local virtual machines to simulate a real production pipeline.

Goal:
Build a complete CI/CD + DevSecOps workflow from code commit to Kubernetes deployment.

Pipeline flow:
GitHub → Jenkins → SonarQube → OWASP Dependency Check → Trivy → Docker → Kubernetes

---

## Infrastructure Design

### VM Architecture

VM1 — Jenkins + Docker
VM2 — SonarQube + PostgreSQL
VM3 — Kubernetes cluster (k3s)

All VMs are connected through a private network for internal communication.

---

## Application Stack

Frontend:

* React

Backend:

* Node.js
* Express

Database:

* MongoDB

Deployment target:

* Kubernetes

---

## CI/CD Pipeline Flow

1. Developer pushes code to GitHub
2. Jenkins pipeline triggers automatically
3. Code checkout from repository
4. SonarQube static code analysis
5. OWASP dependency vulnerability scan
6. Trivy filesystem/image security scan
7. Docker image build
8. Docker image push to DockerHub
9. Kubernetes deployment update
10. Application exposed via service

---

## Security Tools Used

SonarQube:

* Code quality
* Security issues
* Bugs & code smells

OWASP Dependency Check:

* Third-party library vulnerability scanning

Trivy:

* Container & filesystem vulnerability scanning

---

## Kubernetes Architecture

Namespace:

* voyawander

Resources:

* Backend deployment
* MongoDB deployment
* Services (ClusterIP / NodePort)
* Secrets
* Persistent volume claim (MongoDB storage)

Configuration managed through:

* YAML manifests

---

## Environment Configuration Strategy

Important rule:
No hardcoded environment variables inside Docker image.

Environment values provided using:

* Kubernetes Secrets
* Deployment env section

Examples:

* STRIPE_SECRET_KEY
* MONGODB_URI

---

## Major Issues Faced Earlier (Learning History)

SonarQube:

* JVM memory issues
* Permission errors
* Elasticsearch shutdown due to low RAM

PostgreSQL:

* Schema permission denied
* DB connection configuration errors

Jenkins:

* Workspace permission issues
* Git safe.directory warning
* Pipeline syntax mistakes

OWASP:

* NVD update failed without API key
* Scan time extremely long

Docker:

* Environment variables hardcoded inside container
* Required rebuild strategy

Kubernetes:

* CrashLoopBackOff due to wrong Mongo URI
* Mongo image CPU AVX incompatibility
* PVC not created initially
* Secret misconfiguration
* Container env mismatch

Application:

* Mongo connection string format incorrect
* Stripe key missing
* Node backend crash due to missing env

---

## Key Technical Decisions

* MongoDB image pinned to mongo:4.4 (CPU compatibility)
* Kubernetes secrets used for sensitive data
* Docker images version tagged (no latest-only deployments)
* CI/CD pipeline modularized into stages
* Infrastructure separated per VM

---

## Current State

Environment has been reset intentionally.

Plan:
Rebuild complete DevSecOps setup from scratch with clean architecture and proper documentation.

---

## Next Phase Plan

Phase 1:

* Recreate VMs
* Install base dependencies

Phase 2:

* Setup Jenkins + Docker

Phase 3:

* Setup SonarQube + PostgreSQL

Phase 4:

* Setup Kubernetes cluster

Phase 5:

* Rebuild pipeline step-by-step

Phase 6:

* Deploy application

Phase 7:

* Add security scans

Phase 8:

* Implement GitOps (ArgoCD later)

---

## Usage Instructions for AI Tools (Copilot / ChatGPT)

This file provides project architecture context.

Any AI assisting this repository should:

* Follow this infra design
* Avoid hardcoding environment values
* Prefer Kubernetes secrets
* Maintain pipeline modularity
* Ensure production-grade CI/CD flow

---

## Maintainer

DevOps Engineer:
Aryan Singh

Focus:

* DevSecOps
* Kubernetes
* Automation
* CI/CD engineering
