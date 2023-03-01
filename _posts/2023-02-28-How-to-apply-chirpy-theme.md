---
title: How to apply chirpy theme
author: sille_bille
date: 2023-02-28 18:32:00 -0500
categories: [Blogging, Tutorial]
tags: [jekyll, theme, chirpy]
---

### You can apply the chirpy theme to your GitHub blog by following the four steps below.




##### 1) modify /.github/workflows/pages-deploy.yml to enable github action


```console
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
    - name: Setup deploy options
      id: setup
      run: |
        git config --global user.name "GitHub Action"
        git config --global user.email "41898282+github-actions[bot]@users.noreply.github.com"
        if [[ ${GITHUB_REF} = refs/pull/*/merge ]]; then # pull request
          echo "SRC_BRANCH=${GITHUB_HEAD_REF}" >> $GITHUB_OUTPUT
          echo "NO_PUSH=--no-push" >> $GITHUB_OUTPUT
        elif [[ ${GITHUB_REF} = refs/heads/* ]]; then # branch, e.g. master, source etc
          echo "SRC_BRANCH=${GITHUB_REF#refs/heads/}" >> $GITHUB_OUTPUT
        fi
        echo "DEPLOY_BRANCH=gh-pages" >> $GITHUB_OUTPUT
    - name: Deploy to GitHub Pages
      id: deployment
      uses: actions/deploy-pages@v1
 ```

##### 2)give read and write permission to action at YourRepository/settings/actions/general/Workflow permissions

##### 3)select branch to none at YourRepository/settings/Page/Build and deployment/Branch

##### 4)change something and push to main branch, let github action auto generate gh-pages branch. then select it at YourRepository/settings/Page/Build and deployment/Branch
