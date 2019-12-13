# 2019.12.11 atualização 10.15.2
Após a atualização, você pode corrigir o som.Aqui estão as etapas:

> Baixe e substitua a versão mais recente dos seguintes drivers:

* [Clover] (https://github.com/Dids/clover-builder/releases) Baixe a versão `5100` do` CLOVERX64.efi`
* [WhateverGreen_v1.3.5] (https://github.com/acidanthera/WhateverGreen/releases)
* [Lilu_v1.4.0] (https://github.com/acidanthera/Lilu/releases)
* [AppleALC_v1.4.4] (https://github.com/acidanthera/AppleALC/releases)

Atualize diretamente

Após a atualização, sem som, desbloqueie primeiro as permissões do SLE

`` ``
sudo su
sudo mount -uw /
killall Finder
`` ``

Em seguida, use o reparo pop de fone de ouvido conectado, clique duas vezes em `install, clique duas vezes no comando installation.com automático 'e reinicie o computador após a conclusão do reparo.

! [] (https://raw.githubusercontent.com/fengwenhua/ImageBed/master/1576033673_20191211110352592_522659038.png)

---

# 2019.11.9 atualização 10.15.1
Atualize diretamente nas configurações do sistema

Após a conclusão da atualização, percebo que o som desapareceu, Bluetooth, wifi, Little Sun é normal

Corrigir som: atualize lilu applealc Whatevergreen para a versão mais recente

# 2019.11.1 Substitua a placa de rede 1820A
Recentemente, recebi a oferta e é tão suave que um certo tesouro passou 70 oceanos e fez uma 1820A. O tutorial a seguir é sobre instalação

## Nota
Se o seu sistema não estiver instalado corretamente, basta conectar a placa de rede 1820A, ela pode ficar travada, você não pode entrar na interface de instalação ... Portanto, você só pode retirar a placa ~~~

Se você instalou o sistema Catalina, substitua-o por uma placa de rede 1820A, poderá encontrar os dois erros a seguir

### Erro no processo de carregamento do firmware Gfx
`` ``
Basta adicionar -disablegfxfirmware aos parâmetros de inicialização
`` ``

! [] (https://raw.githubusercontent.com/fengwenhua/api-test/master/1573036545_20191020085411554_977482903.png)


### appleintellpssi2ccontroller ftimerservicematching timeout error

Exclua `AppleIntelLpssI2C.kext` e` AppleIntelLpssI2CController.kext` em `/ System / Library / Extensions /`

## Minhas etapas de instalação
1. Instale 10.14.5, entre no sistema
2. Substitua `clover.efi` pelo último, substitua` qualquer que seja verde`, `lilu` e` AppleALC` pelo último
3. Exclua `AppleIntelLpssI2C.kext` e` AppleIntelLpssI2CController.kext` em `/ System / Library / Extensions /`
4. Adicione `-isablegfxfirmware 'aos parâmetros de inicialização
5. Reinicie, insira as configurações do sistema para atualizar o catalina
6. Após a atualização, se você ainda encontrar o segundo erro mencionado acima, retire o cartão, insira Catalina normalmente e exclua os `AppleIntelLpssI2C.kext` e` AppleIntelLpssI2CController 'em `/ System / Library / Extensions /` novamente. kext` e insira o cartão no Catalina
7. O próximo passo é instalar os drivers wifi e Bluetooth

## Etapas de instalação teórica
> Eu o derivei de acordo com as etapas da minha instalação e ainda não o pratiquei

1. Desconecte o 7559 vem com placa de rede wifi
2. Instale 10.14.5, entre no sistema
3. Substitua `clover.efi` como o mais recente, substitua` Whatevergreen`, `lilu` e` AppleALC` como o mais recente
4. Adicione `-isablegfxfirmware 'aos parâmetros de inicialização
5. Insira as configurações do sistema para atualizar o catalina
6. Após a conclusão da atualização, entre primeiro em Catalina normalmente, exclua os arquivos `AppleIntelLpssI2C.kext` e` AppleIntelLpssI2CController.kext` em `/ System / Library / Extensions /`
7. Desligue, conecte a placa de rede 1820A
8. Digite Catalina normalmente
9. Instale o driver

## Instale o driver wifi
Após inserir com êxito a placa de rede 1820A, após entrar na Catalina, o driver é instalado.

Link do tutorial: https://blog.daliansky.net/DW1820A_BCM94350ZAE-driver-inserts-the-correct-posture.html

As etapas gerais são as seguintes:

1. Abra [hackintool] (http://headsoft.com.au/download/mac/Hackintool.zip) e anote o endereço do dispositivo em `PCI`->` BCM4350`

    ! [] (https://raw.githubusercontent.com/fengwenhua/api-test/master/1573036550_20191106182723159_895524893.png)

2. Adicione [AirportBrcmFixup] (https://github.com/acidanthera/AirportBrcmFixup/releases) ao diretório `/ EFI / CLOVER / kexts / Other`
3. Adicione os parâmetros de inicialização em `config.plist`:` brcmfx-country = # a`

    ! [] (https://raw.githubusercontent.com/fengwenhua/api-test/master/1573036552_20191106182802892_1521478475.png)

4. `Dispositivos` ->` Propriedades` adicionam:

    -Adicione o endereço do dispositivo apenas anotado em `Dispositivos` à esquerda:` PciRoot (0x0) / Pci (0x1c, 0x5) / Pci (0x0,0x0) `

    -Adicione à direita:

        | Chave de propriedades | Propriedades Valor | Tipo de valor |
        | -------------- | ---------------------------------- | ---------- |
        | AAPL, nome do slot | WLAN | STRING |
        | compatível | pci14e4,4353 | STRING |
        | device_type | Airport Extreme | STRING |
        modelo | DW1820A (BCM4350) 802.11ac sem fio | STRING |
        | nome | Aeroporto | STRING |

    ! [] (https://raw.githubusercontent.com/fengwenhua/api-test/master/1573036547_20191106181742558_245505540.png)

5. Depois de reiniciar o computador, o wifi está disponível

    ! [] (https://raw.githubusercontent.com/fengwenhua/api-test/master/1573036554_20191106182914024_1400944496.png)

## Instalar o driver Bluetooth
Extraia o [programa especial Bluetooth DW1820A] (http://7.daliansky.net/DW1820A/DW1820A_BT_for_Catalina_v2.5.0.zip) no diretório `/ EFI / CLOVER / kexts / Other` e reinicie-o.

# 7559 preto maçã-10.15
## 0x00 Fora do tópico
Eu vi [黑 果 小兵] dois dias atrás (https://blog.daliansky.net/macOS-Catalina-10.15-19A583-Release-version-with-Clover-5093-original-image-Double-EFI-Version.html ) O pacote de instalação do Catalina foi concluído, mas não terminou no dia seguinte ... Ontem, não tive tempo de ir ao trabalho e finalmente tive tempo de voltar à noite ...

Mas como sinto que o computador ficou travado recentemente, suspeito que instalei algo desarrumado, então desinstalei o 10.14.6 original diretamente e pensei em instalar o Catalina diretamente.

Como resultado, usei o pacote de instalação Catalina do Black Fruit Soldier para ficar preso e não consegui instalá-lo ... Deprimido ... Orz ... Não quero encontrar um bug, não tem como? ?

Não! Acabei de ver que [orange1206] (http://bbs.pcbeta.com/forum.php?mod=viewthread&tid=1818698&highlight=7559) foi atualizado e instalado com sucesso em junho! Atualizou e instalou diretamente! !! Bad !!!!

Então, o que você está esperando? Vamos diretamente ao soldado black fruit para encontrar o pacote de instalação 10.14.5: https://blog.daliansky.net/macOS-Mojave-10.14.5-18F132-official-version-with-Clover- 4928-original-image.html, não pergunte por que, eu fiz isso há muito tempo, então use-o diretamente

Observe que, como o pacote de instalação mais recente do Heiguo Xiaobing não está disponível, ** este tutorial deve atualizar o 10.15 diretamente após a instalação do 10.14.5 e, em seguida, reparar o driver **


> Link de referência: [Tutorial de instalação do Dell 7559 10.14GM (i5 + UEFI)] (http://bbs.pcbeta.com/viewthread-1794485-1-1.html)

> Instale o link 10.14.6: [Dell-7559-10.14.6] (https://blog.csdn.net/A807296772/article/details/101756415)

## 0x01 Configuração do computador
* CPU: i7-6700HQ
* Memória: DDR3L 1600MHz \ * 2
* Disco rígido: 128G + 1T
* Gráficos: GTX960M 4G + Intel HD Graphics 530
* Placa de som: ALC256
* Versão do BIOS: 1.2.8

> Se a configuração for igual ou semelhante, você pode ler


## efeito final 0x02

! [] (https://raw.githubusercontent.com/fengwenhua/ImageBed/master/1570704001.png)

1. A placa de som é perfeita, o fone de ouvido muda automaticamente, exceto o som atual quando inserido ... Atalho do notebook: `F1` mute
