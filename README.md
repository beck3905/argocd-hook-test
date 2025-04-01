# argocd-hook-test
ArgoCD Application with PostSync Hook to demonstrate unexpected behavior

## Setup

1. Apply AppProject to ArgoCD
    ```bash
    kubectl apply -f hook-test.project.yaml
    ```

2. Apply Application to ArgoCD
    ```bash
    kubectl apply -f hook-test.application.yaml
    ```

3. Log into ArgoCD Console
4. Open `hook-test` Application in the ArgoCD Console
   1. Application should be "Out of Sync"
5. Sync the Application

## Expected Behavior

When the Application Syncs, the Deployment should immediately start, but will take about 30 seconds to become "Ready". Once the Deployment is "Ready", the Post Sync Job should spin up and then delete when it is complete.

## Actual Behavior

When the Application Syncs, both the Deployment and the Post Sync Job start immediately. The Deployment takes about 30 seconds to become "Ready" and shortly after the Post Sync Job completes and is deleted.
