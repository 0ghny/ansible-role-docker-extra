# ansible-role-docker-extra
> Configures docker extra stuff

This role

- `docker cleanup`: Install a cleanup operation using a systemd and a systemd timer

## Requirements

* Docker should be installed in your machine, you can do it, using [geerlingguy.docker](https://github.com/geerlingguy/ansible-role-docker) as i do

## Role Variables

Available variables are listed below, along with defautl values (see [defaults/main.yml](./defaults/main.yml))

```shell
docker_extra_dir: "/opt/docker-extra"
# if you want to change the owner and group of the docker_stacks_dir
docker_extra_owner: "{{ ansible_user }}"
# if you want to change the owner and group of the docker_stacks_dir
docker_extra_group: "{{ ansible_user }}"
```

If you wanna change the default user used by ansible by another user present in the box, you can use both `docker_extra_owner` and `docker_extra_group` to make sure that directories are chown to this.


```shell
# cleanup settings
# interval for the docker cleanup service
docker_extra_cleanup_interval: "12h"
docker_extra_cleanup_docker_bin: "/usr/bin/docker"
```

Cleanup settings can be configured using variables above, `docker_extra_cleanup_interval` is the interval to run the [cleanup](./templates/docker-cleanup.service.j2) service to clean docker stuff.

## Credits

* [docker-cleanup.service](./templates/docker-cleanup.service.j2): original idea from https://gist.github.com/mosquito/b23e1c1e5723a7fd9e6568e5cf91180f
* [docker-cleanup.timer](./templates/docker-cleanup.timer.j2): original file getted from https://github.com/louislam/dockge/blob/master/compose.yaml
