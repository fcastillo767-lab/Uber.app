Biblioteca
/
build-apk.yml


name: Generar APK Android

on:
  workflow_dispatch:
  push:
    branches:
      - main

permissions:
  contents: read

jobs:
  generar-apk:
    runs-on: ubuntu-latest

    steps:
      - name: Descargar repositorio
        uses: actions/checkout@v4

      - name: Instalar Java 17
        uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'

      - name: Instalar Flutter estable
        uses: subosito/flutter-action@v2
        with:
          channel: stable
          cache: true

      - name: Preparar proyecto
        run: |
          test -f uber_finanzas_source_v1.zip
          rm -rf app
          mkdir app
          unzip -o uber_finanzas_source_v1.zip -d app
          cd app
          flutter create --platforms=android --project-name uber_finanzas --org com.fcastillo.uberfinanzas .

      - name: Descargar dependencias
        run: |
          cd app
          flutter pub get

      - name: Analizar código
        run: |
          cd app
          flutter analyze

      - name: Compilar APK instalable
        run: |
          cd app
          flutter build apk --release

      - name: Guardar APK para descargar
        uses: actions/upload-artifact@v4
        with:
          name: Uber-Finanzas-APK
          path: app/build/app/outputs/flutter-apk/app-release.apk
          if-no-files-found: error
          retention-days: 30
