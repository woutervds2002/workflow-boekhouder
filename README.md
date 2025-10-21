# workflow-boekhouder
git init
git remote add origin https://github.com/woutervds2002/workflow-boekhouder.git
git add .
git commit -m "Initial commit"
git push -u origin main
services:
  - type: web
    name: workflow-backend
    env: node
    buildCommand: npm install
    startCommand: node server.js
    repo: https://github.com/woutervds2002/workflow-boekhouder
    branch: main
    autoDeploy: true

  - type: static
    name: workflow-frontend
    env: static
    buildCommand: npm install && npm run build --prefix src
    publishPath: src/build
    branch: main
    autoDeploy: true
services:
  - type: web
    name: workflow-backend
    env: node
    buildCommand: npm install --prefix backend
    startCommand: node backend/server.js
    repo: https://github.com/woutervds2002/workflow-boekhouder
    branch: main

  - type: static
    name: workflow-frontend
    env: static
    buildCommand: npm install --prefix frontend && npm run build --prefix frontend
    publishPath: frontend/build
    branch: main
