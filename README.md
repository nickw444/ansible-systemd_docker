## Systemd Docker
Run your docker containers within Systemd at startup.

### Requirements:

 - `Docker` installed on the target
 - `Systemd` installed on the target

### Usage:

**Sample Playbook**

```
- name: "Redis Container"
  tags: redis
  roles:
    - name: nickw444.systemd_docker
      service_name: Redis
      image: redis:latest
      ports:
        - "6379:6379"
      volumes:
        - "/root:/root"
      privileged: no
      command: /bin/bash
```

### Configuration Options
| Option    | Description   | Example   | Default Value     |   |
|-----------------------    |-------------------------------------------------------------------------------------------------------------  |--------------------------------------------------------------------   |-------------------------- |---    |
| docker_binary     | Specify the docker binary to use  |   | `/usr/bin/docker`     |   |
| systemd_services_path     | Specify where to install systemd services     |   | `/lib/systemd/system`     |   |
| service_name  | Specify the service name. **required**    | my-cool-redis-service     |   |   |
| image     | Specify the docker image to use. **required**     | redis:latest  |   |   |
| command   | Override the container's command  | /bin/bash     |   |   |
| privileged    | Enable privileged mode for the container  | yes   | no    |   |
| volumes   | Specify a list of volumes to mount    | ``` volumes:   - "/root:/root" ```    | []    |   |
| volumes_from  | Specify a list of containers to use volumes from  | ``` volumes_from:   - mycontainer ```     | []    |   |
| ports     | Specify a list of ports to expose     |  ``` ports:   - "8080"   - "8080:8080"   - "0.0.0.0:8080:8080" ```    | []    |   |
| links     | Specify other containers to link to   | ``` links:   - "mycontainer:container"   - "container" ```    | []    |   |
| extra_cmd_args    | Specify additional command line arguments     | extra_cmd_args:   - "--volume /root:/root"    | []    |   |
| requires_services     | Specify a service dependency. The Docker service (docker.service) is always specified so you don't need to.   | requires_services:   - "my-other-thing.service"   | []    |   |
| after_services    | Specify After= dependencies. The Docker service (docker.service) is always specified so you don't need to.    | after_services:   - "my-other-thing.service"  | {{ requires_services  }}  |   |