# testing-salt-with-docker
Test your salt states easily in a ready to use dockerized salt master and minion scheme


```
docker-compose up
```

Run a bash session in salt master

```
docker exec -it saltmaster /bin/bash
```

Or just run the commands from your term

```
docker exec -it saltmaster salt-key -L
```
