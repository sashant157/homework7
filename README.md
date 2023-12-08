# Домашнее задание 7. Создание rpm пакета и размещение его в своем репозитории.
homework7.txt вывод в консоли показывающий результат выполнения ДЗ.
строки 2 - 5. Видим созданный командой rpmbuild -bb rpm пакет nginx-1.20.2-1.el8.ngx.x86_64.rpm
строки 22 - 31. Видим страничку репозитория. Репозиторий создан командой createrepo (в директорию репозитория дополнительно добавлен пакет percona-orchestrator-3.2.6-2.el8.x86_64.rpm)
строки 32 -45 видим добавленный репозиторий sashant (создан файл /etc/yum.repos.d/sashant.repo с конфигурацией репозитория) и пакет percona-orchestrator.x86_64 установленный из нового репозитория.

Порядок сборки rpm пакета:
Командой wget скачал исходники ПО пакет SRPM (в моем случае wget https://nginx.org/packages/centos/8/SRPMS/nginx-1.20.2-1.el8.ngx.src.rpm)
Командой rpm -i nginx-1.20.2-1.el8.ngx.src.rpm установил этот пакет. Создался каталог rpmbuild, в нем данные для сборки.
По заданию требуется собрать nginx с openssl, для этого качаем openssl (wget https://github.com/openssl/openssl/archive/refs/heads/OpenSSL_1_1_1-stable.zip) и разархивируем его (unzip ./OpenSSL_1_1_1-stable.zip)
Редактируем nginx.spec (/root/rpmbuild/SPECS/nginx.spec), lj, добавляем опцию --with-openssl=/root/openssl-OpenSSL_1_1_1-stable в строку %define BASE_CONFIGURE_ARGS
Собираем rpm командой rpmbuild -bb /root/rpmbuild/SPECS/nginx.spec
После завершения работы компилятора в каталоге /root/rpmbuild/RPMS/x86_64 видим собраный пакет nginx-1.20.2-1.el8.ngx.x86_64.rpm
