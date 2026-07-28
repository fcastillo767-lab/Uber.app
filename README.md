# Uber Finanzas 1.0

Aplicación Flutter local para registrar viajes, gastos y ganancia neta diaria.

## Funciones incluidas
- Registro de ingresos por viaje.
- Registro de gastos por categoría.
- Resumen diario de ingresos, gastos y ganancia neta.
- Meta diaria y progreso.
- Historial del día.
- Eliminación de movimientos deslizando hacia la izquierda.
- Persistencia local con SQLite.

## Cómo ejecutar
1. Instalar Flutter estable y Android Studio.
2. Abrir esta carpeta en VS Code o Android Studio.
3. Ejecutar:
   ```bash
   flutter pub get
   flutter run
   ```

## Generar APK
```bash
flutter build apk --release
```
El APK se crea en `build/app/outputs/flutter-apk/app-release.apk`.
