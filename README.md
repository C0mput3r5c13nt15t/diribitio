# Diribitio deployment (on a server running Ubuntu)

## Prerequisites
1. [Install Docker](https://docs.docker.com/engine/install/ubuntu/)
2. [Deploy Portainer](https://docs.portainer.io/v/ce-2.11/start/install/server/docker/linux)
3. Set MaxSessions in /etc/ssh/sshd_config (on remote host) to something like 200

## Deploy Diribitio
1. Run `DOCKER_HOST="ssh://user@ip" docker-compose up -d`
2. Run `php artisan migrate --database=landlord --path=database/migrations/landlord/`
3. Create a tenant with `php artisan tenant:create dev dev`
4. Migrate the tenant and invite an admin (`tenant:create_admin`) 
