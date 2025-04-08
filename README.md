# Serveo Self-Hosted - Instalador

Serveo es una herramienta que te permite exponer puertos locales de tu servidor Linux a través de SSH, similar a ngrok pero autoalojado.

## Requisitos
- Sistema Linux (solo arquitectura amd64/x86_64)
- Permisos de root
- Conexión a Internet (para descargar el instalador)

## Instalación

1. **Descargar el instalador**:
   ```bash
   curl -O https://raw.githubusercontent.com/HirCoir/Self-Hosted-Serveo/refs/heads/main/install
   ```

2. **Dar permisos de ejecución**:
   ```bash
   chmod +x install
   ```

3. **Ejecutar el instalador con sudo**:
   ```bash
   sudo bash install
   ```

### Opciones de instalación

Puedes personalizar la instalación con estos argumentos:

- **Especificar puerto** (por defecto: 2222):
  ```bash
  sudo bash install -p 4444
  # o
  sudo bash install --port 4444
  ```

- **Especificar IP pública** (por defecto se autodetecta):
  ```bash
  sudo bash install -h 192.168.1.100
  # o
  sudo bash install --host 192.168.1.100
  ```

- **Eliminar instalación existente**:
  ```bash
  sudo bash install --remove
  ```

## Uso después de la instalación

Una vez instalado, Serveo se ejecutará como un servicio systemd llamado `serveo`.

**Comandos útiles**:

- Ver estado del servicio:
  ```bash
  sudo systemctl status serveo
  ```

- Iniciar/detener/reiniciar:
  ```bash
  sudo systemctl start serveo
  sudo systemctl stop serveo
  sudo systemctl restart serveo
  ```

- Ver logs:
  ```bash
  journalctl -u serveo -f
  ```

## Conexión desde un cliente

Para exponer un puerto local (ej: 3000) a través de tu instancia Serveo:
```bash
ssh -p <PUERTO_SERVEO> -R 8080:localhost:3000 <IP_SERVIDOR>
```

## Ubicación de los archivos
- Binario: `/opt/serveo/serveo`
- Claves SSH: `/opt/serveo/ssh_host_rsa_key`
- Servicio systemd: `/etc/systemd/system/serveo.service`

## Créditos
Desarrollado por HirCoir  
Repositorio: https://github.com/HirCoir/self-hosted-serveo