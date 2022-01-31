# B6.5.1

## Задание

Ссылка: [здесь](./TASK.md)

## Решение

```
# Заполняем перечень удаленных хостов для выполнения задания
vi hosts

# Создаем пользователя, прописываем ssh-публичный ключ (пароль - 1)
ansible-playbook -i hosts --ask-vault-pass playbooks/user-create.yml

# (На удаленных хостах) Проверяем наличие пользователя, файла ключа в домашнем каталоге пользователя
# cat /etc/passwd | grep user1
# cat /home/user1/.ssh/id_rsa.pub

# Устанавливаем-запускаем Postfix
ansible-playbook -i hosts playbooks/postfix.yml --tags 'init postfix'

# (На удаленных хостах) Проверяем наличие сервиса Postfix
# systemctl status postfix

# Удаляем Postfix
ansible-playbook -i hosts playbooks/postfix.yml --tags 'drop postfix'

# (На удаленных хостах) Проверяем наличие сервиса Postfix
# systemctl status postfix
