Actúa como un equipo experto en DevOps y CI/CD.
Objetivo: Crear un pipeline en GitHub Actions que se dispare únicamente cuando haya un push a una rama con un Pull Request abierto.
Tareas:
1. Configura el workflow en `.github/workflows/pipeline.yml` con el nombre `Backend CI/CD Pipeline`.
2. Define los jobs secuenciales:
   - `backend-tests`: ejecutar `npm install` y luego `npm test` para validar el backend.
   - `backend-build`: ejecutar `npm install` y luego `npm run build` para generar el build del backend.
   - `deploy-ec2`: conectarse vía SSH a un servidor EC2 usando `appleboy/ssh-action`, hacer `git pull origin ${{ github.ref }}`, instalar dependencias en modo producción (`npm install --production`) y reiniciar el servicio con `pm2 restart backend`.
3. Asegúrate de que cada job tenga la condición `if: github.event.pull_request != null` para que solo se ejecute si el push está asociado a un Pull Request abierto.
4. Usa `needs` para que los jobs se ejecuten en orden: primero tests, luego build, finalmente deploy.
5. Configura las credenciales de EC2 (`EC2_HOST`, `EC2_USER`, `EC2_SSH_KEY`) como GitHub Secrets y consúmelas en el job de despliegue.
6. El pipeline debe ser limpio, comentado y listo para producción.
