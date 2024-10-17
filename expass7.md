The goal of this lecture is to get familiar with Docker.
I will look both at using "containerized" standard software as well as "containerizing" applications.

First want to say about DOCKER;
A Docker image is an executable package that includes everything needed to run a piece of software, such as the code, runtime, 
libraries, environment variables, and configuration files. 

It serves as a blueprint for creating Docker containers, 
which are instances of these images running in isolated environments

Docker images are composed of several key components:

Layers: Immutable filesystem layers stacked to form a complete image. Each layer represents a set of file changes or additions.

Base Image: The foundational layer, often a minimal OS or runtime environment.

Dockerfile: A text file containing instructions to build a Docker image.

Image ID: A unique identifier for each Docker image.

Tags: Labels used to manage and version Docker images


## TASK 1##    I try to find out what -p and -e arguments you have to pass to the docker run command?


My set-up --- (I doing before from expass1), docker system - docker is installed on my computer! 
Using a Dockerized application: PostgreSQL

On of the main advantages of Docker is that it greatly simplifies running such software. Instead of manually installing PostgreSQL - docker image of PostgreSQL.docker pull postgresThe image name postgres gets implicitly expanded to docker.io/library/postgres:latest, i.e. the image tagged as latest, stored in the repository postgres, 
maintained by Docker Inc. (library) and hosted on Docker Hub (docker.io).

Using the PostgreSQL docker image; i try to find which prt and where is the place off the fil, to this prosject the Europe port 
for the find ting and argument -p-e docker run

docker run -p {{ Find out what Port you have to expose... }} \
 -e {{ Find out what environment variables you have to set... }} \
 -d --name my-postgres --rm postgres
 

![Skjermbilde 2024-10-17 114607](https://github.com/user-attachments/assets/4af08f26-bd62-4258-bb2a-2a62d48a16f2)


![Skjermbilde 2024-10-17 113841](https://github.com/user-attachments/assets/72fdbd2a-db87-4a07-a1cc-ef3f0ac5d40e)

![Skjermbilde 2024-10-17 114019](https://github.com/user-attachments/assets/e3573379-b0bb-43c6-ba54-98dc084381d4)

## TASK 2##  Building you own dockerized application 

Now, write Dockerfile in this following steps:

Start with the FROM <base image> line,
copy your application into the image via the COPY instruction,
and install dependencies as well as package the application by executing the respective shell commands with RUN statements (tips: the gradle bootJar task can be "handy" here).
The final instruction should be the CMD instruction that starts the Spring Boot Java application.
Implementation("org.postgresql:postgresql:42.7.4")

the target to find container -e represent user and password while -d represent database; -rm postgres (not the default behavior), a
dd two variables to postgres and docker image run,

Then using gradle defines image, which obtained from gradle and runs RUN gradle bootJar.

JPA client (best practice).

CREATE USER jpa_client WITH PASSWORD 'secret';
After the new user has been created, switch over to the Java project. To change the database from H2 to PostgreSQL, you first have to add the correct JDBC driver. Open the build.gradle.kts file and add the following dependency:

![Skjermbilde 2024-10-17 114223](https://github.com/user-attachments/assets/85955040-5134-423f-b244-810259a0ed3f)


![Skjermbilde 2024-10-17 114622](https://github.com/user-attachments/assets/caf11c3e-b1cd-4459-87f3-ec5ed6a97d9c)


implementation("org.postgresql:postgresql:42.7.4")
Also, replace the old connection parameters in the persistence.xml from the JPA example, which used H2:

![Skjermbilde 2024-10-17 114607](https://github.com/user-attachments/assets/7441b467-4fa3-49de-b61c-b97e6a843c6b)


![Skjermbilde 2024-10-17 114223](https://github.com/user-attachments/assets/bca6b9a9-af4e-47aa-b2ec-b24203aafc33)

![Skjermbilde 2024-10-17 114607](https://github.com/user-attachments/assets/318c905e-1061-4a19-95b0-254826369378)







![Skjermbilde 2024-10-17 114622](https://github.com/user-attachments/assets/ca00186a-3e38-4d63-9c7b-c980de632ebd)


