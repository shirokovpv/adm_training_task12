# adm_training_task12
<h1 align="center">Занятие 12. Vagrant-стенд для обновления ядра и создания образа системы</h1>
<h3 class="western"><a name="_heading=h.h6i87lkp3f19"></a> <span style="font-family: Roboto, serif;"><span style="font-size: small;">Описание домашнего задания</span></span></h3>
<p><span style="font-weight: 400;">1) Запустить ВМ с помощью Vagrant.</span></p>
<p><span style="font-weight: 400;">2) Обновить ядро ОС из репозитория ELRepo.</span></p>
<p><span style="font-weight: 400;">3) Оформить отчет в README-файле в GitHub-репозитории.</span></p>
<p align="left">&nbsp;</p>
<h3 class="western"><a name="_heading=h.df570rpzx1qg"></a><span style="font-family: Roboto, serif;"><span style="font-size: small;">Используемые ОС</span></span></h3>
<p style="line-height: 108%; margin-bottom: 0.28cm;" align="justify"><span style="font-family: Roboto, serif;">Хостовая ОС Ubuntu 24.04 Desktop. Гостевая ОС centos8. VirtualBox версия 7.0.16_Ubuntu r162802</span></span></p>
<p style="line-height: 100%; margin-bottom: 0cm;">&nbsp;</p>
<h3 class="western"><span style="font-family: Roboto, serif;"><span style="font-size: small;">Выполнение</span></span></h3>
<p>Ввиду невозможности в нынешних реалиях воспользоваться стандартными репозиториями Vagrant (в РФ они сейчас не доступны), предложено обходное решение. Использован репозиторий, развернутый на&nbsp;<a href="https://vagrant.elab.pro/" rel="nofollow">https://vagrant.elab.pro/</a></p>
<p>Так как официальный пакет последней версии Vagrant также не доступен для скачивания, пакет взят оттуда же. Версия 2.3.5.</p>
<img width="411" height="88" alt="image" src="https://github.com/user-attachments/assets/7591c684-f543-4bf6-bfa8-3706a7648c97" />
<p align="left">&nbsp;</p>
<p>Для подключения репозитория надо добавить в Vagrant-файл строку:</p>
<p><code>ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro'</code></p>
<p>И изменить box_name и box_version (как в репозитории, если туда зайти).</p>
<img width="259" height="137" alt="image" src="https://github.com/user-attachments/assets/e8572ad5-f77d-4d9c-97a8-dc2e49975a62" />
<p align="left">&nbsp;</p>
<p><span style="font-weight: 400;">Создадим каталог kernel_update, а в нем Vagrantfile, в котором будут указаны параметры нашей ВМ:</span></p>
<img width="803" height="761" alt="image" src="https://github.com/user-attachments/assets/24e0c03b-7d95-4dbc-ac4d-3e3cfabf7a5b" />
<p align="left">&nbsp;</p>
<p><span style="font-weight: 400;">Созданный файл добавляю к этому отчету. После создания Vagrantfile запустим виртуальную машину командой vagrant up</span></p>
<p>shirokovpv@SPB300:~/kernel_update$ vagrant up<br />Bringing machine 'kernel-update' up with 'virtualbox' provider...<br />==&gt; kernel-update: Box 'centos/8' could not be found. Attempting to find and install...<br /> kernel-update: Box Provider: virtualbox<br /> kernel-update: Box Version: 1.0.0<br />==&gt; kernel-update: Loading metadata for box 'centos/8'<br /> kernel-update: URL: https://vagrant.elab.pro/centos/8<br />==&gt; kernel-update: Adding box 'centos/8' (v1.0.0) for provider: virtualbox<br /> kernel-update: Downloading: <a href="http://vagrant.elab.pro:80/centos/8/1.0.0/virtualbox">http://vagrant.elab.pro:80/centos/8/1.0.0/virtualbox</a></p>
<p>...</p>
<p>==&gt; kernel-update: Machine booted and ready!<br />==&gt; kernel-update: Checking for guest additions in VM...<br /> kernel-update: No guest additions were detected on the base box for this VM! Guest<br /> kernel-update: additions are required for forwarded ports, shared folders, host only<br /> kernel-update: networking, and more. If SSH fails on this machine, please install<br /> kernel-update: the guest additions and repackage the box to continue.<br /> kernel-update: <br /> kernel-update: This is not an error message; everything may continue to work properly,<br /> kernel-update: in which case you may ignore this message.<br />==&gt; kernel-update: Setting hostname...<br />shirokovpv@SPB300:~/kernel_update$ </p>
<p><span style="font-weight: 400;">Видим в VirtualBox, что ВМ установлена и запущена:</span></p>
<img width="1098" height="541" alt="image" src="https://github.com/user-attachments/assets/090dd81d-e95c-4875-b016-0a9d261cef95" />
<p align="left">&nbsp;</p>
<h4><strong>Обновление ядра</strong></h4>
<p><span style="font-weight: 400;">Подключаемся по ssh к созданной виртуальной машине. Для этого в каталоге с нашим Vagrantfile вводим команду </span><span style="font-weight: 400;">vagrant ssh</span></p>
<p><span style="font-weight: 400;">Перед работами проверим текущую версию ядра:</span></p>
<img width="517" height="103" alt="image" src="https://github.com/user-attachments/assets/e2eb1d02-7d9d-4233-8c36-26a639c26d69" />
<p align="left">&nbsp;</p>
<h4>4.18.0-240.1.1.el8_3.x86_64</h4>
<p><span style="font-weight: 400;">Далее подключим репозиторий, откуда возьмём необходимую версию ядра: sudo yum install -y </span><a href="https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm"><span style="font-weight: 400;">https://www.elrepo.org/elrepo-release-8.el8.elrepo.noarch.rpm</span></a> </h4>
<p>&nbsp;</p>
<p>*********</p>
<p>Возможно, проблема с этой конкретной версией, установленной из этого репозитория - команда не хотела выполняться.</p>
<p>После небольшого траблшутинга -</p>
<pre>cd /etc/yum.repos.d/<br />sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*<br />sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*<br />sudo yum update -y<br /></pre>
<p>- все пошло как надо</p>
<p>*********</p>
<img width="798" height="732" alt="image" src="https://github.com/user-attachments/assets/674f21e6-42aa-4145-9c35-6a5b90d59048" />
<p align="left">&nbsp;</p>
<p><span style="font-weight: 400;">В репозитории есть две версии ядер:</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">kernel-ml &mdash; свежие и стабильные ядра</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">kernel-lt &mdash; стабильные ядра с длительной версией поддержки, более старые, чем версия ml.</span></li>
</ul>
<p><span style="font-weight: 400;">Установим последнее ядро из репозитория elrepo-kernel:</span></p>
<p><span style="font-weight: 400;">sudo yum --enablerepo elrepo-kernel install kernel-ml -y</span></p>
<p>[vagrant@kernel-update ~]$ sudo yum --enablerepo elrepo-kernel install kernel-ml -y<br />Failed to set locale, defaulting to C.UTF-8<br />ELRepo.org Community Enterprise Linux Reposito 119 kB/s | 217 kB 00:01 <br />ELRepo.org Community Enterprise Linux Kernel R 3.8 MB/s | 4.5 MB 00:01 <br />Last metadata expiration check: 0:00:01 ago on Sat Sep 6 19:16:18 2025.<br />Dependencies resolved.<br />===============================================================================<br /> Package Arch Version Repository Size<br />===============================================================================<br />Installing:<br /> kernel-ml x86_64 6.16.5-1.el8.elrepo elrepo-kernel 158 k<br />Installing dependencies:<br /> kernel-ml-core x86_64 6.16.5-1.el8.elrepo elrepo-kernel 67 M<br /> kernel-ml-modules x86_64 6.16.5-1.el8.elrepo elrepo-kernel 63 M</p>
<p>Transaction Summary<br />===============================================================================<br />Install 3 Packages</p>
<p>Total download size: 130 M<br />Installed size: 175 M<br />Downloading Packages:<br />(1/3): kernel-ml-6.16.5-1.el8.elrepo.x86_64.rp 490 kB/s | 158 kB 00:00 <br />(2/3): kernel-ml-core-6.16.5-1.el8.elrepo.x86_ 16 MB/s | 67 MB 00:04 <br />(3/3): kernel-ml-modules-6.16.5-1.el8.elrepo.x 8.9 MB/s | 63 MB 00:06 <br />-------------------------------------------------------------------------------<br />Total 17 MB/s | 130 MB 00:07 <br />ELRepo.org Community Enterprise Linux Kernel R 1.6 MB/s | 1.7 kB 00:00 <br />GPG key at file:///etc/pki/rpm-gpg/RPM-GPG-KEY-elrepo.org (0xBAADAE52) is already installed<br />ELRepo.org Community Enterprise Linux Kernel R 3.0 MB/s | 3.1 kB 00:00 <br />Importing GPG key 0xEAA31D4A:<br /> Userid : "elrepo.org (RPM Signing Key v2 for elrepo.org) &lt;secure@elrepo.org&gt;"<br /> Fingerprint: B8A7 5587 4DA2 40C9 DAC4 E715 5160 0989 EAA3 1D4A<br /> From : /etc/pki/rpm-gpg/RPM-GPG-KEY-v2-elrepo.org<br />Key imported successfully<br />Running transaction check<br />Transaction check succeeded.<br />Running transaction test<br />Transaction test succeeded.<br />Running transaction<br /> Preparing : 1/1 <br /> Installing : kernel-ml-core-6.16.5-1.el8.elrepo.x86_64 1/3 <br /> Running scriptlet: kernel-ml-core-6.16.5-1.el8.elrepo.x86_64 1/3 <br /> Installing : kernel-ml-modules-6.16.5-1.el8.elrepo.x86_64 2/3 <br /> Running scriptlet: kernel-ml-modules-6.16.5-1.el8.elrepo.x86_64 2/3 <br /> Installing : kernel-ml-6.16.5-1.el8.elrepo.x86_64 3/3 <br /> Running scriptlet: kernel-ml-core-6.16.5-1.el8.elrepo.x86_64 3/3 <br />dracut: Disabling early microcode, because kernel does not support it. CONFIG_MICROCODE_[AMD|INTEL]!=y</p>
<p>Running scriptlet: kernel-ml-6.16.5-1.el8.elrepo.x86_64 3/3 <br /> Verifying : kernel-ml-6.16.5-1.el8.elrepo.x86_64 1/3 <br /> Verifying : kernel-ml-core-6.16.5-1.el8.elrepo.x86_64 2/3 <br /> Verifying : kernel-ml-modules-6.16.5-1.el8.elrepo.x86_64 3/3</p>
<p>Installed:<br /> kernel-ml-6.16.5-1.el8.elrepo.x86_64 kernel-ml-core-6.16.5-1.el8.elrepo.x86_64 kernel-ml-modules-6.16.5-1.el8.elrepo.x86_64</p>
<p>Complete!<br />[vagrant@kernel-update ~]$</p>
<p><span style="font-weight: 400;">Параметр </span><span style="font-weight: 400;">--enablerepo elrepo-kernel </span><span style="font-weight: 400;">указывает что пакет ядра будет запрошен из репозитория elrepo-kernel.</span></p>
<p><span style="font-weight: 400;">Уже на этом этапе можно перезагрузить нашу виртуальную машину и выбрать новое ядро при загрузке ОС.&nbsp;</span></p>
<p><span style="font-weight: 400;">Если требуется, можно назначить новое ядро по умолчанию вручную:</span></p>
<p><span style="font-weight: 400;">1) Обновить конфигурацию загрузчика:</span></p>
<p><span style="font-weight: 400;">sudo grub2-mkconfig -o /boot/grub2/grub.cfg</span></p>
<p><span style="font-weight: 400;">2) Выбрать загрузку нового ядра по умолчанию:</span></p>
<p><span style="font-weight: 400;">&nbsp;&nbsp;&nbsp;</span> <span style="font-weight: 400;">sudo grub2-set-default 0</span></p>
<img width="798" height="115" alt="image" src="https://github.com/user-attachments/assets/8a8b3ad4-730f-4012-a4ea-300cd3c157bd" />
<p>&nbsp;</p>
<p><span style="font-weight: 400;">Далее перезагружаем нашу виртуальную машину с помощью команды </span><span style="font-weight: 400;">sudo reboot</span></p>
<p><span style="font-weight: 400;">После перезагрузки снова проверяем версию ядра (версия должна стать новее):</span></p>
<p><span style="font-weight: 400;">[vagrant@kernel-update ~]$ uname -r</span></p>
<img width="798" height="111" alt="image" src="https://github.com/user-attachments/assets/fdc42b77-b21f-45c8-aeed-051896ababfa" />
<p>&nbsp;</p>
<p>Новое ядро <b>6.16.5-1.el8.elrepo.x86_64</b></p>
<p>Задание завершено.</p>
