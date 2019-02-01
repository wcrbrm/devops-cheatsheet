# Docker

```
# Show every processi - with formatting
sudo docker ps --format "table {{.ID}}\t{{.Image}}\t{{.Command}}\t{{.Status}}\t{{.Ports}}"

# Prune everything
sudo docker system prune -af && sudo docker volume prune -f

```
