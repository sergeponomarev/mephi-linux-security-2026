Раздел 1. Создание пользователя
1.1 Создаем группу student 
1.2 Создаем пользователя user1 
1.3 Изменяем срок действия пароля (chage)
1.4 su - user1
Раздел 2. Мониторинг файлов и процессов
2.1 Мониторинг файлов: sudo find / -perm -4000 -type f   (-4000 маска S бита)
Пример вывода:
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/polkit-1/polkit-agent-helper-1
/usr/bin/newgrp
/usr/bin/umount
/usr/bin/mount
/usr/bin/passwd
/usr/bin/su
/usr/bin/gpasswd
/usr/bin/chfn
/usr/bin/chsh
/usr/bin/fusermount3
/usr/bin/sudo
/home/user1/newcat
/home/sitroot/newcat
2.2 Мониторинг процессов:  ps -eo euid,ruid,pid,user,comm | awk '$1 == 0 && $2 != 0' (ищем euid рутовый, а ruid усеровский)
                           0  1000    3411 root     passwd  - в другом терминале запущен passwd
Раздел 3. Изучение механизма set-UID
3.1 Копируем утилиту cat в /home/user1/newcat(cp)
3.2 Меняем владельца и группу на root (chown)
3.3 Устанавливаем бит SetUID для newcat (chmod)
3.4 Смотрим newcat /etc/shadow    Access: (0640/-rw-r-----) - результат - видимость содержимого
Раздел 4. Изучение механизма привилегий

Раздел 5. Изучение механизма sudo
5.1 Добавляем user1 в группу sudo : sudo usermod -aG sudo user1
5.2 su - user1
5.3 sudo timedatectl
