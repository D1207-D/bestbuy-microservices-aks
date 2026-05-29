# bestbuy-microservices-aks

Cloud-native e-commerce platform built with microservices, deployed on Azure Kubernetes Service with Azure OpenAI integration and event-driven order processing.

![Kubernetes](https://img.shields.io/badge/Kubernetes-AKS-326CE5?style=flat&logo=kubernetes)
![Azure](https://img.shields.io/badge/Azure-OpenAI-0078D4?style=flat&logo=microsoftazure)
![Docker](https://img.shields.io/badge/Docker-Containers-2496ED?style=flat&logo=docker)

## Overview

Microservices-based retail platform deployed on AKS, modelled on a Best Buy e-commerce architecture. Features AI-generated product descriptions and images via Azure OpenAI, event-driven order processing via Azure Service Bus, and simulated customer/worker traffic for load testing.

## Architecture

![Architecture Diagram](Architecture.png)

## Services

| Service | Language | Description |
|---|---|---|
| store-front | Vue.js | Customer-facing storefront for browsing and ordering |
| store-admin | Vue.js | Employee portal for inventory and order management |
| order-service | JavaScript | Order creation and queue integration |
| product-service | Rust | Product CRUD operations |
| makeline-service | Golang | Reads order queue and processes completions |
| ai-service | Python | AI-generated product descriptions and images via Azure OpenAI |
| virtual-customer | Rust | Simulates customer order traffic |
| virtual-worker | Rust | Simulates employee order processing |
| MongoDB | - | Product and order data persistence |
| Azure Service Bus | - | Reliable message queue for order management |

## Docker Images

| Service | Image |
|---|---|
| store-front | [daniyal1207/best-buy-store-front](https://hub.docker.com/r/daniyal1207/best-buy-store-front) |
| order-service | [daniyal1207/best-buy-order-service](https://hub.docker.com/r/daniyal1207/best-buy-order-service) |
| product-service | [daniyal1207/best-buy-product-service](https://hub.docker.com/r/daniyal1207/best-buy-product-service) |
| makeline-service | [daniyal1207/best-buy-makeline-service](https://hub.docker.com/r/daniyal1207/best-buy-makeline-service) |
| store-admin | [daniyal1207/best-buy-store-admin](https://hub.docker.com/r/daniyal1207/best-buy-store-admin) |
| ai-service | [daniyal1207/best-buy-ai-service](https://hub.docker.com/r/daniyal1207/best-buy-ai-service) |
| virtual-customer | [daniyal1207/best-buy-virtual-customer](https://hub.docker.com/r/daniyal1207/best-buy-virtual-customer) |
| virtual-worker | [daniyal1207/best-buy-virtual-worker](https://hub.docker.com/r/daniyal1207/best-buy-virtual-worker) |

## Prerequisites

- Azure subscription
- Azure CLI
- kubectl
- Docker

## Deployment

1. Create AKS cluster and connect:

    az aks get-credentials --resource-group bestbuydani --name bestbuyclusterdani
    kubectl get nodes

2. Deploy ConfigMaps and Secrets:

    kubectl apply -f Deployment Files/config-maps.yaml
    kubectl apply -f Deployment Files/secrets.yaml

3. Deploy all services:

    kubectl apply -f Deployment Files/aps-all-in-one.yaml

4. Deploy virtual traffic simulators:

    kubectl apply -f Deployment Files/admin-tasks.yaml

5. Verify deployment:

    kubectl get pods
    kubectl get services

## Scaling and Monitoring

Scale a service:

    kubectl scale deployment order-service --replicas=3

Monitor resource usage:

    kubectl top pods
    kubectl top nodes

## Demo

[Watch demo video](https://youtu.be/_CSSFdaQpxM)
