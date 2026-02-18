Задание 1  



---



1. Скачал  
2. Согласно файлу .gitignore, личную секретную информацию (логины, пароли, ключи, токены) допустимо сохранять в файле: personal.auto.tfvars  
3. "result": "VVNl08gvCjKTjYjw"  
4. В ресурсе docker\_image отсутствует имя и обязательный параметр name, имя ресурса docker\_container не может начинаться с цифры, ссылка на несуществующий ресурс random\_password.random\_string\_FAKE  

5\.  



```bash 



resource "docker\_image" "nginx" {

&nbsp; name         = "nginx:latest"

&nbsp; keep\_locally = true

}



resource "docker\_container" "nginx\_container" {

&nbsp; image = docker\_image.nginx.image\_id

&nbsp; name  = "example\_${random\_password.random\_string.result}"



&nbsp; ports {

&nbsp;   internal = 80

&nbsp;   external = 9090

&nbsp; }

}



```

&nbsp; 

CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES

0ee9b35efb07   5cdef4ac3335   "/docker-entrypoint.…"   9 seconds ago   Up 5 seconds   0.0.0.0:9090->80/tcp   example\_VVNl08gvCjKTjYjw  



6\.  

&nbsp; 

CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES

d57aad1f111d   5cdef4ac3335   "/docker-entrypoint.…"   3 seconds ago   Up 3 seconds   0.0.0.0:9090->80/tcp   hello\_world  

&nbsp; 

Ключ -auto-approve автоматически применяет изменения без запроса подтверждения от пользователя.  

Его польза: aвтоматизация в CI/CD пайплайнах, быстрое применение однотипных изменений.  

&nbsp; 

7\.  

```bash



{

&nbsp; "version": 4,

&nbsp; "terraform\_version": "1.12.2",

&nbsp; "serial": 11,

&nbsp; "lineage": "3bf8b946-1af4-e1d3-1ac5-708c7a6d7bdd",

&nbsp; "outputs": {},

&nbsp; "resources": \[],

&nbsp; "check\_results": null

}



```

&nbsp; 

8\. Подтверждение из документации Terraform провайдера docker: keep\_locally (Boolean) If true, the image will be kept locally after the resource is destroyed. Defaults to false. Это означает, что при уничтожении ресурса (terraform destroy) образ Docker не удаляется с локальной машины, а только удаляется из управления Terraform.  



resource "docker\_image" "nginx" {

&nbsp; name         = "nginx:latest"

&nbsp; keep\_locally = true  # Этот параметр предотвращает удаление образа

}



