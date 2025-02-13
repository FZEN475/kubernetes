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





















