# kubernetes
## Description
* Кластер устанавливается через kubeadm [kubeadm_init.conf](https://github.com/FZEN475/kubernetes/blob/main/config/kubeadm_init.conf).
  * InitConfiguration
    * Ключ шифрования сертификатов передаётся через секрет.
  * KubeletConfiguration
    * Включен swap.
    * Управление ресурсами systemd.
* Управление сетью [tigera calico](https://docs.tigera.io/calico/latest/about/).
  * bgp включен.
  * xVlan включен.
* Внешний etcd.
## Network
| Сеть             | Назначение                 | Comment |
|:-----------------|:---------------------------|:--------|
| 192.170.0.0/23   | Сервисы.                   |         |
| 192.180.0.0/23   | Вся подсеть подов.         |         |
| 192.180.0.0/25   | Подсеть управляющих подов. |         |
| 192.180.0.128/25 | Подсеть подов хранилищ.    |         |
| 192.180.1.0/25   | Подсеть подов разработки.  |         |
| 192.180.1.128/25 | Подсеть подов продакшена.  |         |

## Resource Balancings

<details><summary> table </summary>

<table class="tg"><thead>
  <tr>
    <th class="tg-9wq8" rowspan="3">request<br>items</th>
    <th class="tg-0pky" colspan="2">control01</th>
    <th class="tg-0pky" colspan="2">control02</th>
    <th class="tg-0pky" colspan="2">control3</th>
    <th class="tg-0pky" colspan="2">storage01</th>
    <th class="tg-0pky" colspan="2">dev01</th>
    <th class="tg-0pky" colspan="2">prod01</th>
  </tr>
  <tr>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
    <th class="tg-0pky">cpu</th>
    <th class="tg-0pky">ram</th>
  </tr>
  <tr>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
    <th class="tg-ti2n">10000</th>
    <th class="tg-ti2n">6144</th>
  </tr></thead>
<tbody>
  <tr>
    <td class="tg-qm20">prometheus</td>
    <td class="tg-ti2n">1400</td>
    <td class="tg-ti2n">1536</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">grafana</td>
    <td class="tg-ti2n">400</td>
    <td class="tg-ti2n">400</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">dashboard</td>
    <td class="tg-ti2n">400</td>
    <td class="tg-ti2n">800</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">NFS</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">150</td>
    <td class="tg-ti2n">128</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">cert-manager</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">600</td>
    <td class="tg-ti2n">512</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">ingress</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1000</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">vault</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1500</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">external-secrets</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1500</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">reloader</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">250</td>
    <td class="tg-ti2n">128</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">gitlab</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">2000</td>
    <td class="tg-ti2n">2080</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1000</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-ti2n">1500</td>
    <td class="tg-ti2n">1536</td>
  </tr>
  <tr>
    <td class="tg-qm20">minio</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1000</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">pgsql</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1000</td>
    <td class="tg-ti2n">1024</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">pgadmin</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">1000</td>
    <td class="tg-ti2n">512</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
  <tr>
    <td class="tg-qm20">redis</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-ti2n">3450</td>
    <td class="tg-ti2n">2136</td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
    <td class="tg-qm20"></td>
  </tr>
</tbody></table>

</details>

## Dependency
* [Образ](https://github.com/FZEN475/ansible-image)
* [Library](https://github.com/FZEN475/ansible-library)
* <details><summary> .env </summary>

  ```properties
  TERRAFORM_REPO="https://github.com/FZEN475/kubernetes.git"
  #GIT_EXTRA_PARAM="-btemp_branch"
  SECURE_SERVER=""
  SECURE_PATH=""
  LIBRARY="https://github.com/FZEN475/ansible-library.git"
  ``` 
  </details>
* <details><summary> secrets </summary>

  ```yaml
  secrets:
    - id_ed25519
    - CERTIFICATE_KEY # Секрет с ключём шифрования сертификатов kubernetes (AES key of size 32 bytes)
  ```
  </details>

## Stages
### [reset](https://github.com/FZEN475/kubernetes/blob/main/playbooks/_1_kubeadm/_0_reset_cluster.yaml)
* Расформирование kubernetes кластера.
* Удаление драйверов cni драйвера.
* Сброс iptables.
* Удаление vlan-интерфейсов.
* Сброс всей маршрутизации и Vlan.
* Перезапуск docker (для восстановления swarm).
### [init](https://github.com/FZEN475/kubernetes/blob/main/playbooks/_1_kubeadm/_1_init.yaml)
* Проверка доступности etcd.
* Если сбрасываем базу.
  * Очистка __**всей**__ базы etcd.
* Создание рабочей [kubeadm_init.conf](https://github.com/FZEN475/kubernetes/blob/main/config/kubeadm_init.conf).
* Создание мастера и join ссылок (в контейнере). 
* [Перенастройка coredns](https://github.com/FZEN475/kubernetes/blob/main/config/Corefile) под текущую инфраструктуру.
### [join](https://github.com/FZEN475/kubernetes/blob/main/playbooks/_1_kubeadm/_2_join.yaml)
* Присоединение node к кластеру.
### [network](https://github.com/FZEN475/kubernetes/blob/main/playbooks/_1_kubeadm/_3_network.yaml)
* Маркировка node.
* [Установка tigera-operator](https://github.com/FZEN475/kubernetes/blob/main/config/calico-values.yaml).
* [Настройка IPPool](https://github.com/FZEN475/kubernetes/blob/main/config/calico-networks.yaml).
### [Дополнительно](https://github.com/FZEN475/kubernetes?tab=readme-ov-file#Troubleshoots)

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
      <td>После присоединения NODE в статусе NotReady</td>
      <td>

После изменения конфигурации cni драйвера нужно перезапустить containerd.
</td>
  </tr>
</table>





