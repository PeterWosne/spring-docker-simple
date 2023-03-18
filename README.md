# spring-docker-simple 

mvnw package && java -jar target/spring-docker-simple-0.0.1-SNAPSHOT.jar  упаковать приложение в jar-файл и запустить

---------------------------------------------------------------------------------------------------------------------------

в корне проекта создать Dockerfile(содержит инструкции для сборки образа)

FROM openjdk:17-alpine                                                    образ создается на основе alpine linux и openjdk17

ARG JAR_FILE=target/spring-docker-simple-0.0.1-SNAPSHOT.jar                            переменная содержит путь к jar-архиву

WORKDIR opt/app                                                               назначаем рабочую директорию и переходим в нее

COPY ${JAR_FILE} app.jar                                             копируем jar-файл в директорию и задаем ему имя app.jar

ENTRYPOINT ["java","-jar","app.jar"]                                                                               запускаем

----------------------------------------------------------------------------------------------------------------------------

docker build -t spring-docker-simple:0.0.1 .   собираем образ. Точка указывает на расположение Dockerfile(текущая директория)

docker images                                                                                              посмотреть образы

docker run -d -p 8080:8080 -t spring spring-docker-simple:0.0.1    
-d значит в фоновом режиме

docker -ps      список всех запущенных контейенеров
docker -ps -a   список всех контейенеров

docker logs --follow e43ht37rhuob  следить за логами запущенного контейнера

docker stop
docker stop $(docker ps -a -q) остановить все

docker rm    удалить контейнер
docker rmi   удалить контейнер вместе с образом
