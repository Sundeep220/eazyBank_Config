# EazyBank Configuration Repository

This repository contains the centralized configuration for the **eazyBank** application, which consists of three microservices: **accounts**, **loans**, and **cards**.

## Overview

- Each microservice has environment-specific configuration variables managed here.
- For each microservice, configurations are organized into three environments:
  - **default** (common base configuration)
  - **production (prod)**
  - **quality assurance (qa)**
- This allows seamless separation and management of environment-specific settings.

## Configuration Management

- The repository is used by the **Spring Cloud Config Server** to serve configuration properties to the microservices.
- Configurations are stored in a Git-managed repository, enabling version control and auditability of all configuration changes.

## Dynamic Refresh of Configuration

- **Spring Cloud Monitor** is integrated to listen for configuration changes via GitHub Webhooks configured on this repository.
- When a configuration change is pushed, the webhook notifies the Spring Cloud Config Server.
- The Config Server then triggers a refresh event through **Spring Cloud Bus** using **RabbitMQ** as the message broker.
- This mechanism ensures that all running microservices receive updated configuration values automatically without requiring restarts.

## Naming Conventions

- Configuration files follow a naming convention based on microservice name and environment, for example:
  - `<microservice>-<environment>.yml`
- This structure allows the Config Server to serve the appropriate configuration based on service and profile.
- For example:
  - `account.yml`
  - `accounts-prod.yml`
  - `accounts-qa.yml`
  - `loans.yml`
  - `loans-prod.yml`
  - `loans-qa.yml`
  - `cards.yml`
  - `cards-prod.yml`
  - `cards-qa.yml`

- This naming pattern allows the Spring Cloud Config Server to serve the correct configuration file based on the microservice name and active environment profile.

---

This setup ensures consistent, centralized, and dynamic configuration management for the entire eazyBank microservices ecosystem.
