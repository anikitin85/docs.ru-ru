---
title: Практическое руководство. Установка и настройка компонентов активации WCF
description: Узнайте, как настроить службу активации процессов Windows (WAS) в Windows Vista для размещения служб WCF, не взаимодействующих по протоколу HTTP.
ms.date: 03/30/2017
helpviewer_keywords:
- HTTP activation [WCF]
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
ms.openlocfilehash: 84a0dcc4fed28ebd7a536bdabfcdc389be6072d8
ms.sourcegitcommit: 358a28048f36a8dca39a9fe6e6ac1f1913acadd5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/23/2020
ms.locfileid: "85246887"
---
# <a name="how-to-install-and-configure-wcf-activation-components"></a>Практическое руководство. Установка и настройка компонентов активации WCF

В этом разделе описываются шаги, необходимые для настройки службы активации Windows (также известной как WAS) в Windows Vista для размещения служб Windows Communication Foundation (WCF), не передающих сетевые протоколы HTTP. Настройка предполагает следующие шаги.

- Установите (или подтвердите установку) компоненты активации WCF.

- Настройте WAS на поддержку отличных от HTTP протоколов. Следующая процедура настраивает Windows Vista для активации TCP.

После установки и настройки WAS см. раздел [как разместить службу WCF в WAS](how-to-host-a-wcf-service-in-was.md) для процедур создания службы WCF, предоставляющей конечную точку, которая не является КОНЕЧНОЙ точкой HTTP.

## <a name="to-install-the-wcf-non-http-activation-components"></a>Установка компонентов активации WCF, работающих по отличному от HTTP протоколу

1. В меню **Пуск** выберите пункт **Панель управления**.

2. Последовательно выберите **Программы**, **Программы и компоненты**.

3. В меню **задачи** выберите команду **Включение или отключение компонентов Windows**.

4. Найдите узел WinFX, выберите и разверните его.

5. Выберите пункт **WCF-компоненты активации, отличные от HTTP** и сохраните параметр.

## <a name="to-configure-the-was-to-support-tcp-activation"></a>Настройка WAS на поддержку протокола TCP

1. Для поддержки активации по net.tcp веб-узел по умолчанию необходимо сначала привязать к порту net.tcp. Это можно сделать с помощью Appcmd.exe, который устанавливается вместе с набором средств управления IIS 7,0. В окне командной строки с правами администратора выполните следующую команду.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > Эта команда представляет собой одну строку текста. Она добавляет привязку узла к протоколу net.tcp в веб-узел по умолчанию, ожидающему передачи данных по протоколу TCP на порту 808 с любым именем узла.

2. Несмотря на то что все приложения в узле имеют общую привязку к протоколу net.tcp, включать поддержку net.tcp можно для каждого приложения отдельно. Для включения протокола net.tcp для данного приложения необходимо выполнить следующую команду из командной строки с правами администратора.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp
    ```

    > [!NOTE]
    > Эта команда представляет собой одну строку текста. Эта команда обеспечивает доступ к \<*WCF Application*> приложению или с помощью `http://localhost/<WCF Application>` и `net.tcp://localhost/<WCF Application>` .

     Удалите привязку сайта к протоколу net.tcp, добавленную ранее для данного образца.

     Для удобства два нижеописанных действия выполняются в пакетом файле RemoveNetTcpSiteBinding.cmd, расположенном в каталоге с образцами.

    1. Удалите протокол net.tcp из списка разрешенных протоколов, выполнив следующую команду в окне командной строки с правами администратора.

        ```console
        %windir%\system32\inetsrv\appcmd.exe set app
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
        ```

        > [!NOTE]
        > Эта команда представляет собой одну строку текста.

    2. Удалите привязку узла к протоколу net.tcp, выполнив следующую команду в окне командной строки с повышенными привилегиями:

        ```console
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
        --bindings.[protocol='net.tcp',bindingInformation='808:*']
        ```

        > [!NOTE]
        > Эта команда представляет собой одну строку текста.

## <a name="to-remove-nettcp-from-the-list-of-enabled-protocols"></a>Удаление протокола net.tcp из списка разрешенных протоколов

1. Для того чтобы удалить протокол net.tcp из списка разрешенных протоколов, необходимо выполнить следующую команду в окне командной строки с правами администратора.

    ```console
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http
    ```

    > [!NOTE]
    > Эта команда представляет собой одну строку текста.

## <a name="to-remove-the-nettcp-site-binding"></a>Удаление привязки узла к протоколу net.tcp

1. Для того чтобы удалить привязку узла к протоколу net.tcp, необходимо выполнить следующую команду в окне командной строки с правами администратора:

    ```console
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"
    -bindings.[protocol='net.tcp',bindingInformation='808:*']
    ```

    > [!NOTE]
    > Эта команда представляет собой одну строку текста.

## <a name="see-also"></a>См. также

- [Активация TCP](../samples/tcp-activation.md)
- [Активация MSMQ](../samples/msmq-activation.md)
- [Активация NamedPipe](../samples/namedpipe-activation.md)
- [Функции размещения Windows Server App Fabric](https://docs.microsoft.com/previous-versions/appfabric/ee677189(v=azure.10))
