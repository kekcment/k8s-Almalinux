Файлы в папке test-kube-claster выполнятются в следующем порядке
1) cd test-kube-claster
2) ansible-playbook -i hosts kube-dependencies.yml -K
3) ansible-playbook -i hosts master.yml -K
4) ansible-playbook -i hosts worker.yml -K

Файлы в папке k8s

Запускается через:

ansible-playbook -i inventory main.yaml -K

Билд от 03.05.23

1) Перед запуском
При запуске редаткируем файл inventory (Вид: ( tst-alma-k8s-m1 ansible_ssh_host=192.168.33.9 ansible_user=localadmin) нужен только для файла hosts) 

2) Pre-installation options запускать только один раз. 
После рекомендую мьютить.

3) Install cri-docker
cri-docker устанавливается через костыль. Цыфры в скобках ссылаются на рабочий мануал* . 
При появлении ошибок связанных с firewall-ом/не поднимается мастер нода, замьютить сроки "when" на цыфрах 10-12

4) Установка kuberadm && worker-node
Основная ошибка которая может быть, не подключаются ноды.
Один из путей решения. Необходимо удалить следующие файлы на всех нодах:
/var/lib/etcd
/var/lib/kubelet
/etc/kubernetes
/etc/cni/net.d
Так же удалить весь пакет кубера: sudo yum remove -y kubelet kubeadm kubectl --disableexcludes=Kubernetes
Возможно будет написан отдельный плэйбук по удалению следов кубера.

5) Setup monitoring не подключен
Так же для его настройки придется подключать ansible-galaxy

F.A.Q и ссылки: 

Ссылка на оригинальный репозиторий:  https://github.com/jaanhio/k8s-playbook 
Ссылка на рабочий мануал: https://phoenixnap.com/kb/kubernetes-almalinux
Полезная ссылка: https://habr.com/ru/companies/domclick/articles/682364/

Pyhton3.9 не ставить. Вылетают ошибки.
Весь процесс дебага пройден. На голое железо/вм, с первого раза должно ставиться. Основная проблема с подключением нод (решение выше)

Ранчер в сделку не входил, но комманда установки: 
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher:v2.5.17
