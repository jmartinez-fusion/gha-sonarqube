# Integración de Github Actions y SonarQube

Este repositorio contiene un ejemplo de cómo integrar [Sonarqube](https://docs.sonarsource.com/sonarqube/10.3/) con [Github Actions](https://docs.github.com/es/actions) ejecutando Sonarqube en local y exponiéndolo al exterior con [ngrok](https://ngrok.com/)

## Contexto
Este repositorio forma parte del contenido de mis cursos de udemy:
* [Domina Github Actions](https://www.udemy.com/course/domina-github-actions/?referralCode=CBFBAF72C38BE758CFE1)
* [Domina Sonarqube](https://www.udemy.com/course/domina-sonarqube/?referralCode=EF59257E7D8DC3026D6D)

Si te interesa aprender más sobre Sonarqube o Github Actions, Puedes ver si hay promociones vigentes para los cursos en la sección de cursos de [devopsbrains.com](https://devopsbrains.com/cursos/)


## Prerrequisitos
* Docker
* Docker compose
* Node.js (solo si quieres construir la aplicación docker en local)
* Cuenta de Github con Github Actions habilitado
* Cuenta de ngrok

# Uso del ejemplo
* Crea un fork de este repositorio en tu cuenta de Github
* Clona el código en local y ajusta la configuración de ngrok
    * Modifica el fichero ngrok.yaml para indicar tu dominio de ngrok en el campo `domain`. Para saber más sobre [ngrok](https://youtu.be/UW8BObHdi08)    
    * Crea un fichero .env a la raíz del repositorio para indicar tu clave de ngrok
```
NGROK_AUTHTOKEN=<aqui tu token>
```
* Lanza Sonarqube + ngrok en local con `docker-compose up`
* Crea un token para el análisis de proyectos en [sonarqube](http://localhost:9000/account/security)
* Crea secretos para tu url y token de sonar para tu repositorio de Github
    * SONAR_TOKEN - El token que acabas de generar en el apartado de seguridad de SonarQube
    * SONAR_HOST_URL - Tu dominio de ngrok, donde estás exponiendo Sonarqube al mundo
* Lanza la acción en el apartado "Actions" de tu repositorio en Github. Con un push a la rama main o manualmente
* Si todo sale bien deberías de poder consultar el resultado en tu instancia de [SonarQube](http://localhost:9000/dashboard?id=hello-sonar-ngrok)

## Construir la aplicación probada en local
En la carpeta src

* Descargar las dependencias npm

```shell
npm i
```


* Generar la imagen docker. 

```shell
docker build . --tag dice:1.0
```

* Ejecutar la aplicación

```shell
docker run --rm -p 8080:8080 dice:1.0
```

* Ver el resultado de la tirada de dados en http://localhost:8080/