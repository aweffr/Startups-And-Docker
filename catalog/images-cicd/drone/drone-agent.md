# Drone-Agent

## 简介



## EXPOSE

无

## 命令

{% tabs %}
{% tab title="Docker" %}

{% endtab %}

{% tab title="Swarm" %}
```bash
docker service create --replicas 1 \
--name drone-runner \
--network staging \
-e TZ=Asia/Shanghai \
-e DRONE_RPC_PROTO=http \
-e DRONE_RPC_HOST=drone \
-e DRONE_RPC_SECRET=MWckgvhjqg4E3eQ0ptg2X4iNC6oQiyU4LLvO4eXFFuHtrTkIy2vwcAc3erB5f9reM \
-e DRONE_RUNNER_CAPACITY=2 \
-e DRONE_RUNNER_NAME=drone-runner \
--mount type=bind,source=/var/run/docker.sock,target=/var/run/docker.sock \
drone/drone-runner-docker
```
{% endtab %}
{% endtabs %}



##  参考

