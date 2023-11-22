---
layout: default
title: OpenID Connect (OIDC)
has_children: false
permalink: /docs/cloud/cicd/oidc
grand_parent: Cloud
parent: CI/CD Pipeline
has_toc: true
---


# OpenID Connect (OIDC)
To deploy changes to AWS through GitHub Actions, GitHub Actions need to have the permission to access our AWS resources.  

One possible approach is to store the AWS credentials in GitHub Secrets, but it could lead to a potential security risk, as it is always not the best practice to store a credentials in a third-party service.  

The alternative approach is to use OpenID Connect (OIDC) to enable GitHub Actions to access our AWS resources with a short-lived token.  And to do so, an OIDC identity provider has been previously setup in AWS, and a dedicated IAM role has been created to grant GitHub Actions the relevant permissions to access our AWS resources.  

(See GitHub [documentation](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect) for more details about OIDC on GitHub Actions)