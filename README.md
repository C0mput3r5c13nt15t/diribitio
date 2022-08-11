# diribitio-deployment (on a server running Ubuntu)

## Prerequisites
1. [Install Docker](https://docs.docker.com/engine/install/ubuntu/)
2. [Deploy Portainer](https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux) (optional)
3. Set MaxSessions in /etc/ssh/sshd_config (on remote host) to something like 200

## Deploy Diribitio
1. Copy the .env.example file to .env and modify it
2. Copy the laravel.env.example file in the backend folder to laravel.env and modify it
3. Run `DOCKER_HOST="ssh://user@ip" docker-compose up -d`
4. Run `php artisan migrate --database=landlord --path=database/migrations/landlord/`
5. Create a tenant with `php artisan tenant:create dev dev`
6. Migrate the tenant and invite an admin (`tenant:create_admin`)
7. Run `php artisan storage:link` in the project directory
