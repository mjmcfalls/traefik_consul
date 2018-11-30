# traefik_consul

Currently random notes from configuring Traefik and consul.

docker service create --name=www --network=consul-overlay --label traefik.port=80 --label traefik.frontend.rule="Path:/" --replicas=3 httpd

docker service create --name whoami0 --label traefik.port=80 --label-add traefik.frontend.rule="Path:/whoami"  --replicas 3 --network consul-overlay containous/whoami

#Get container names matching filter
docker ps --filter "name=consul*" --format "{{ .Names }}"

# Get IP Address
$(docker inspect --format '{{ $network := index .NetworkSettings.Networks "consul-overlay" }}{{$network.IPAddress}}' consulbootstrap)

# Get IP Address matching name 
$(docker inspect --format '{{ $network := index .NetworkSettings.Networks "consul-overlay" }}{{$network.IPAddress}}' $(docker ps --filter "name=consul*" --format "{{ .Names }}"))
