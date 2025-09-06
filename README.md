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




