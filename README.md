name: Build
on:
  push:
  workflow_dispatch:
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: 21
      - name: Unzip and build
        run: |
          unzip -q *.zip
          cd vclient
          chmod +x gradlew
          ./gradlew build --no-daemon
      - uses: actions/upload-artifact@v4
        with:
          name: vclient-jar
          path: vclient/build/libs/vclient-1.0.0.jar
