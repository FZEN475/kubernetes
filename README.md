# kubernetes
## Описание
* Кластер устанавливается через kubeadm [kubeadm_init.conf]().
  * InitConfiguration
    * Ключ шифрования сертификатов передаётся через секрет.
  * KubeletConfiguration
    * Кластер использует swap.
    * Управление ресурсами systemd.
    * Включен endpoint логов.
* Управление сетью [tigera calico](https://docs.tigera.io/calico/latest/about/).
  * bgp включен.
  * xVlan включен.
* etcd внешний.
## Network
| Сеть             | Назначение                | Comment |
|:-----------------|:--------------------------|:--------|
| 192.170.0.0/23   | Сервисы                   |         |
| 192.180.0.0/23   | Вся подсеть подов         |         |
| 192.180.0.0/25   | Подсеть управляющих подов |         |
| 192.180.0.128/25 | Подсеть подов хранилищ    |         |
| 192.180.1.0/25   | Подсеть подов разработки  |         |
| 192.180.1.128/25 | Подсеть подов продакшена  |         |

## Resource Balancing



## Dependency
| Дополнительно           | Значение                                              | Comment                                 |
|:------------------------|:------------------------------------------------------|:----------------------------------------|
| Образ                   | [ansible](https://github.com/FZEN475/ansible-image)   |                                         |
| Библиотеки              | [Library](https://github.com/FZEN475/ansible-library) |                                         |
| secrets.CERTIFICATE_KEY | AES key of size 32 bytes                              | Секрет с ключем шифрования сертификатов |
## Stages
### [reset]()
* Сброс всех NODE.
* Удаление драйверов cni (calico).
* Сброс всей маршрутизации и Vlan.
### [init]()
* Очистка базы данных etcd (опционально).
* 















## Troubleshoots

<!DOCTYPE html>
<table>
  <thead>
    <tr>
      <th>Проблема</th>
      <th>Решение</th>
    </tr>
  </thead>
  <tr>
      <td>Из контейнера не определяется DNS имя без домена.</td>
      <td>
На хосте докера:  
/etc/docker/daemon.json

```json
{
  "dns": ["192.168.2.1","8.8.8.8"]
}
```
</td>
  </tr>
  <tr>
  </tr>
  <tr>
      <td>CoreDNS не видит домен fzen.pro</td>
      <td>

[Причина]()
```shell
kubectl edit -n kube-system cm/coredns
```
```yaml
data:
  Corefile: |
    .:53 {
        errors
        log
        health {
            lameduck 5s
        }
        ready
        template IN A fzen.pro {
            match "(^\w*[.]|^.*[.]pages[.])fzen[.]pro[.]$"
            answer "{{ .Name }}  60  IN  A  192.168.2.2"
            fallthrough
        }
        kubernetes fzen.pro in-addr.arpa ip6.arpa {
            pods insecure
            fallthrough in-addr.arpa  ip6.arpa
            ttl 30
        }
        prometheus :9153
        forward . /etc/resolv.conf {
            max_concurrent 1000
        }
        cache 30
        loop
        reload
        loadbalance
    }

```

[//]: # (TODO: Не удалось сделать forward на верхний DNS. Домен fzen.pro управляется kubernetes и любые попытки добавить правила для fzen.pro мешают работе плагина kubernetes.)

</td>
  </tr>
  <tr>
  </tr>
</table>





