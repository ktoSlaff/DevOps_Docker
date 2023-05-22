# Contents

1. [Part I Ready-made docker](#part-1-ready-made-docker)
2. [Part II Operations with container](#part-2-operations-with-container)
3. [Part III Mini web server](#part-3-mini-web-server)
4. [Part IV Your own docker](#part-4-your-own-docker)
5. [Part V Dockle](#part-5-dockle)
6. [Part VI Basic Docker Compose](#part-6-basic-docker-compose)


В качестве результата работы по первым двум задачам должен быть предоставлен отчет.
В каждой части задания указано, что должно быть помещено в отчёт, после её выполнения.
Это могут быть ответы на вопросы, скриншоты и т.д.

В качестве результата работы по третьей задаче должны быть предоставлены исходные файлы для запуска веб-сервера.

В качестве результата работы по четвёртой и пятой задачам должны быть предоставлены докерфайлы.

В качестве результата работы по шестой задаче должен быть предоставлен файл *docker-compose.yml* и нужные для его запуска докерфайлы (если они не были предоставлены ранее).

- В репозиторий, в папку src, должен быть загружен отчёт с расширением .md.
- В отчёте должны быть выделены все части задания, как заголовки 2-го уровня.
- В рамках одной части задания всё, что помещается в отчёт, должно быть оформлено в виде списка.
- Каждый скриншот в отчёте должен быть кратко подписан (что показано на скриншоте).
- Все скриншоты обрезаны так, чтобы была видна только нужная часть экрана.
- На одном скриншоте допускается отображение сразу нескольких пунктов задания, но они все должны быть описаны в подписи к скриншоту.
- В репозиторий, в папку src/server, должны быть загружены исходные файлы для запуска веб-сервера из третьего задания.
- В репозиторий, в папку src, должны быть загружены итоговые докерфайлы для запуска образов из четвёртого и пятого заданий.
- В репозиторий, в папку src, должен быть загружен *docker-compose.yml* шестого задания.
- Необходимо быть готовым продемонстрировать решение вживую при необходимости.

## Part 1. Ready-made docker
- Taking the official docker image from **nginx** and download it using `docker pull nginx`
- Checking for the docker image with `docker images`
- Runing docker image with `docker run -d [image_id|repository]`
- Checking that the image is running with `docker ps`
    ![Alt text](images/part_1_pull_check_run_nginx_images_check_nginx_container.png)
- View container information with `docker inspect [container_id|container_name]` \
    ![Alt text](images/part_1_inspect_docker_container_0.png)
    ![Alt text](images/part_1_inspect_docker_container_1.png)
    ![Alt text](images/part_1_inspect_docker_container_2.png)
    ![Alt text](images/part_1_inspect_docker_container_3.png)
    ![Alt text](images/part_1_inspect_docker_container_4.png)
    ![Alt text](images/part_1_inspect_docker_container_5.png)
- From the command output define and write in the report the container size, list of mapped ports and container ip:
    - Size:  "ShmSize": 67108864
    - Ports: "ExposedPorts": { "80/tcp": {} }
    - IP:    "IPAddress": "172.17.0.2"
- Stop docker image with `docker stop [container_id|container_name]`
- Check that the image has stopped with `docker ps`
- Runing docker with ports 80 and 443 in container, mapped to the same ports on the local machine, with *run* command
- Checking that the **nginx** start page is available in the browser at *localhost:80*
    ![Alt text](images/part_1_stop_and_check_container_run_mapped_80_443_and_check_nginx_start_page.png)
- Restarting docker container with `docker restart [container_id|container_name]`
- Checking in any way that the container is running
    ![Alt text](images/part_1_restarting_and_checking_docker_container_is_running.png)
## Part 2. Operations with container

- Read the *nginx.conf* configuration file inside the docker container with the *exec* command
    ![Alt text](images/part_2_reading_conf_file_inside_container.png)
- Create a *nginx.conf* file on a local machine
- Configure it on the */status* path to return the **nginx** server status page
    ![Alt text](images/part_2_creating_nginx_conf_file_on_local_machine.png)
- Copying the created *nginx.conf* file inside the docker image using the `docker cp` command
- Restart **nginx** inside the docker image with *exec*
- Check that *localhost:80/status* returns the **nginx** server status page
    ![Alt text](images/part_2_copying_created_nginx_conf_file_to_container_and_check_it.png)
- Export the container to a *container.tar* file with the *export* command
    ![Alt text](images/part_2_export_container_archive_and_check_it.png)
- Stop the container
    ![Alt text](images/part_2_stoping_container_and_check_it.png)
- Delete the image with `docker rmi [image_id|repository]`without removing the container first
- Delete stopped container
    ![Alt text](images/part_2_deleting_image_and_stopped_container_and_check_it.png)
- Importing the container back using the *import* command
- Runing the imported container
- Checking that *localhost:80/status* returns the **nginx** server status page
    ![Alt text](images/part_2_importing_container_run_it_and_check_server_status.png)

## Part 3. Mini web server

- Write a mini server in **C** and **FastCgi** that will return a simple page saying `Hello World!`
    ![Alt text](images/part_3_mini_server_code_on_c.png)
- Run the written mini server via *spawn-fcgi* on port 8080
    ![Alt text](images/part_3_script_for_mini_server_run.png)
    ![Alt text](images/part_3_runing_mini_server_by_sript.png)
- Write your own *nginx.conf* that will proxy all requests from port 81 to *127.0.0.1:8080*
    ![Alt text](images/part_3_creating_new_nginx_conf.png)
- Reloading container and checking that browser on *localhost:81* returns the page "Hello World!"
    ![Alt text](images/part_3_reloading_nginx_and_checking_returnig_page_hello_world.png)
    ![Alt text](images/part_3_checking_returnig_page_hello_world_in_browser.png)
- Put the *nginx.conf* file under *./nginx/nginx.conf* (you will need this later)
    ![Alt text](images/part_3_putting_nginx_conf_to_nginx.png)

## Part 4. Your own docker

- 1) builds mini server sources on FastCgi from [Part 3](#part-3-mini-web-server)
- 2) runs it on port 8080
- 3) copies inside the image written *./nginx/nginx.conf*
- 4) runs **nginx**
    ![Alt text](images/part_4_dockerfile.png)
- Build the written docker image with `docker build`, specifying the name and tag
- Check with `docker images` that everything is built correctly
    ![Alt text](images/part_4_building_image_name_tag.png)
    ![Alt text](images/part_4_building_image_name_tag_1.png)
    ![Alt text](images/part_4_checking_image_name_tag.png)
- Run the built docker image by mapping port 81 to 80 on the local machine and mapping the *./nginx* folder inside the container to the address where the **nginx** configuration files are located
- Check that the page of the written mini server is available on localhost:80
    ![Alt text](images/part_4_run_builded_image_name_tag_and_checking_localhost_80.png)
- Add proxying of */status* page in *./nginx/nginx.conf* to return the **nginx** Яserver status
    ![Alt text](images/part_4_adding_localhost_80_status_nginx_conf.png)
- Restart docker image(container)
*If everything is done correctly, after saving the file and restarting the container, the configuration file inside the docker image should update itself without any extra steps
- Check that *localhost:80/status* now returns a page with **nginx** status
    ![Alt text](images/part_4_checking_localhost_80_status.png)

## Part 5. **Dockle**

- Check the image from the previous task with `dockle [image_id|repository]`
    ![Alt text](images/part_5_dockle_checking_image.png)
- Fix the image so that there are no errors or warnings when checking with **dockle**
    ![Alt text](images/part_5_dockle_checking_image_after_dockerfile_fix.png)
    ![Alt text](images/part_5_hello_world_is_up_and_shown_on_localhost.png)

## Part 6. Basic **Docker Compose**

There, you've finished your warm-up. Wait a minute though...
Why not try experimenting with deploying a project consisting of several docker images at once?

**== Task ==**

- Write a *docker-compose.yml* file, using which:
    1) Start the docker container from [Part 5](#part-5-dockle) _(it must work on local network, i.e., you don't need to use **EXPOSE** instruction and map ports to local machine)_
    2) Start the docker container with **nginx** which will proxy all requests from port 8080 to port 81 of the first container
- Map port 8080 of the second container to port 80 of the local machine
    ![Alt text](images/part_6_docker_compose_yml.png)
    ![Alt text](images/part_6_nginx6_conf_for_nginx_container.png)
- Stop all running containers
- Build and run the project with the `docker-compose build` and `docker-compose up` commands
- Check that the browser returns the page you wrote on *localhost:80* as before
    ![Alt text](images/part_6_stopping_all_container.png)
    ![Alt text](images/part_6_delete_all_container_run_docker_compose_and_check_hello_world.png)