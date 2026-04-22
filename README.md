# k3s-resume-platform-gitops

GitOps repository for the K3s Resume Platform.

This repo stores the desired deployment state for the RSS/Resume application across development and production environments. It is intentionally separated from the application source repository so build activity and deployment state remain distinct.

## Purpose

This repository demonstrates a practical GitOps deployment model:

- development image updates are propagated automatically
- production promotion is handled separately and pinned by immutable digest
- deployment state is versioned, reviewable, and auditable through Git history

## Repo Structure

- `clusters/my-cluster/apps/dev/rss-api/`
  - development deployment state
  - updated through Flux image automation
- `clusters/my-cluster/apps/prod/rss-api/`
  - production deployment state
  - updated through explicit promotion commits

## Dev Auto-Update Flow

Development updates are automated through Flux image automation.

High-level flow:

1. A new application image is built and pushed from the app repo.
2. Flux detects the new image.
3. The dev manifest is updated in this repository.
4. The cluster reconciles to the updated dev state.

This provides a visible Git trail for automated dev changes.

## Prod Promotion Flow

Production is promoted separately from development.

High-level flow:

1. A known image is selected for promotion.
2. The production manifest is updated explicitly.
3. The production deployment references the image by immutable digest.
4. Git history preserves the exact production promotion event.

This keeps production promotion controlled and inspectable.

## What This Repo Proves

- GitOps-based separation between build state and deployment state
- automated dev image update flow
- explicit production promotion workflow
- immutable production image references by digest
- auditable deployment history through Git commits

## What Is Not Claimed

This repository does not currently claim verified Kubernetes admission policy enforcement or other controls that are not directly implemented and evidenced here.

The goal is to keep the public project story accurate and defensible.