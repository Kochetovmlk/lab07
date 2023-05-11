# lab07
Предупреждение!В проекте реализованы две ветки, основная main (В ней будет реализован сам отчёт) и master (В ней реализован функционал лабораторной).

Цель - изучене систем автоматизации развёртывания и управления приложениями на примере Docker.

1) Установлю docker:
sudo apt update
sudo apt install -y curl
curl -fsSL https://get.docker.com/ | sudo sh

2) Создам директорию с проектом и перейду в нее:
mkdir my_project
cd my_project

3) Создам файл Dockerfile:

FROM ubuntu:18.04 

RUN apt update 
RUN apt install -yy gcc g++ cmake
 
RUN mkdir hello_world 
COPY . hello_world/ 
WORKDIR hello_world 
RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install 
RUN cmake --build _build 
RUN cmake --build _build --target install
 
ENTRYPOINT ./_build/hello_world_app

4) Создам файл CMakeLists.txt:
 cmake_minimum_required(VERSION 3.2) 
 
project (project_hw) 
 
add_executable(hello_world_app 
    hello_world.cpp 
) 
 
install(TARGETS hello_world_app hello_world_app RUNTIME DESTINATION /bin)

5) Создам файл hello_world:
 #include <iostream> 
 
int main() { 
    std::cout << "Hello world" << std::endl; 
}
  
  6) Соберу Docker-образ из файла Dockerfile с помощью команды:
   sudo docker build -t my_project .
  
  7)Запуск контейнера на основе созданного образа с помощью команды:
   sudo docker run my_project
  
  Приложение внутри контейнера вывело на экран фразу "Hello world".
