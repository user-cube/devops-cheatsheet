---
title: CI/CD
layout: home
nav_order: 4
has_children: true
permalink: docs/cicd
last_modified_date: 2024-01-07
---

# CI/CD

CI/CD, which stands for Continuous Integration and Continuous Deployment (or Continuous Delivery), encompasses a set of practices and tools utilized by software development teams to automate the process of building, testing, and deploying software changes. The primary objective is to enhance the efficiency, reliability, and speed of the development and release process.

![CI/CD](https://user-cube.github.io/devops-cheatsheet/assets/images/cicd.png)

## Continuous Integration (CI):

- Integration: Developers frequently merge their code changes into a shared repository (version control system, like Git) multiple times a day.
- Automated Build: Following each integration, an automated build process is triggered to compile the code and create an executable or deployable artifact.
- Automated Testing: Automated tests (unit tests, integration tests, etc.) are executed to ensure that the new changes haven't introduced errors or regressions.

The key benefits of CI include early detection of integration issues, faster feedback for developers, and a more stable codebase.

## Continuous Deployment/Delivery (CD):

- Continuous Deployment: Involves automatically deploying the built and tested code changes to production environments. This means that changes are automatically pushed to production as soon as they pass all tests in the CI pipeline.
- Continuous Delivery: Similar to Continuous Deployment, but the deployment to production is a manual decision. Once the code has passed all tests, it is ready for deployment, but a human or automated approval process is needed before pushing changes to production.

CD aims to make the release process more reliable and less error-prone by automating the deployment process. It allows teams to release new features or fixes more frequently and with greater confidence.

To implement CI/CD, various tools and technologies are used, including version control systems (e.g., Git), build automation tools (e.g., Jenkins, Travis CI), automated testing frameworks (e.g., JUnit, Selenium), and containerization technologies (e.g., Docker).

Overall, CI/CD is a critical component of modern software development practices, enabling teams to deliver high-quality software rapidly and efficiently.
