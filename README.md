Файлы в папке test-kube-claster выполнятются в следующем порядке
1) cd test-kube-claster
2) ansible-playbook -i hosts kube-dependencies.yml -K
3) ansible-playbook -i hosts master.yml -K
4) ansible-playbook -i hosts worker.yml -K

Файлы в папке k8s

Запускается через:
1) ansible-playbook -i inventory main.yaml -K

Должен отработать без ошибок. (Работа продолжается 02.05.23)