# Notesapp
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: 18

      - name: Install & test server
        working-directory: server
        run: |
          npm ci
          npm run test --if-present

      - name: Build client
        working-directory: client
        run: |
          npm ci
          npm run build
