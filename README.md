# Docker Workshop
Materiály a postupy probírané při Docker Workshopu.

## Užitečné odkazy
### Dokumentace
- https://docs.docker.com/
### Nástroje pro správu
- Portainer - http://portainer.io/
- Shipyard - https://shipyard-project.com/

## Nasazení aplikace do Dockeru
- předpoklady: 
  - nainstalovaný Docker (např. na virtuálním stroji ve VirtualBoxu)
  - Java aplikace ve formátu .war (např. aplikace docker.war)
  - prosdílená složka v lokálním PC do virtuálního stroje (např. lokální PC - C:\tmp; virtuální stroj - /media/sf_tmp)
      - při vývoj webových aplikací v Javě se build projektu do souboru ve formátu .war provádí do složky v projektu - název bývá "**output**", "**target**", apod.

1. spuštění Docker kontejneru s Tomcatem 8.5.11 na pozadí, napamovanou složkou a forwardovaným portem 8080
    - syntaxe: `docker run [PARAMETRY] DOCKER_IMAGE [PRIKAZ] [ARGUMENTY]`
    - příkaz: `docker run -d --name dockerapp -v /media/sf_tmp/target:/usr/local/tomcat/webapps -p 8080:8080 tomcat:8.5.11`
      - docker run = vytvoření a spuštění nového kontejneru
        - parametry:
           - **-d** = spuštění kontejneru na pozadí
           - **--name** = nastavení jména kontejneru
           - **-v source:target** = namapování lokální složky do specifikovaného umístění v kontejneru
           - **-p OUT:IN** = forwardování vnitřního portu kontejneru (IN) na venkovní port (OUT) hosta, na kterém Docker služba běží
           - **tomcat:8.5.11** = konkrétní obraz ze kterého se vytvoří nový kontejner
2. zobrazení webové aplikace v prohlížeči
    - syntaxe: http://<IP_ADRESA_VIRTUALNIHO_STROJE>:<OUT_PORT>/<APLIKACE>
    - příklad: http://192.168.56.101:8080/docker
