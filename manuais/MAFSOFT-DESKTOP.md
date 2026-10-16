# Manual de Instalação MAFSOFT - DESKTOP

**Versão 1.0** · 14/10/2026

## Objetivo

Este manual define o padrão único de instalação do MAFSOFT, válido a partir da versão 2.85. A instalação é feita uma vez por computador; depois disso o sistema se atualiza sozinho.

É para quem instala: representantes, suporte MAFSOFT e clientes com equipe de TI própria.

## Requisitos do computador

| Item | Exigência |
| --- | --- |
| Sistema | Windows 10 ou 11 (Windows Server 2016 ou superior para servidor) |
| .NET Framework | 4.8 (já vem no Windows 10 atualizado e no 11) |
| PowerShell | Liberado para executar (usado pela atualização automática) |
| Internet | Acesso a github.com e mafsoft.com.br (ver Liberações) |
| Permissão | Usuário com gravação na pasta do sistema; administrador só na instalação |
| Certificado digital | A1 (arquivo .pfx e senha) ou A3 (token/cartão com driver instalado) |
| Espaço em disco | 2 GB livres (programa, XMLs baixados e cópia da versão anterior) |

## Pasta padrão

Instale em **C:\\EDESK**, direto na raiz do disco. Se o cliente preferir outro nome (ex.: C:\\SISTEMA), pode usar, desde que siga as regras abaixo.

- **Nunca em Arquivos de Programas (C:\\Program Files):** o Windows bloqueia gravação ali, e a atualização automática deixa de funcionar.
- **Nunca na Área de Trabalho, Downloads ou OneDrive:** sincronização de nuvem trava arquivos durante a atualização.
- **Os dados ficam na mesma pasta do programa** (configuração, banco local, XMLs, pastas por CNPJ). Para backup ou troca de computador, copie a pasta inteira.
- **Uma pasta por computador.** Todos os programas MAFSOFT ficam juntos nela; a atualização troca todos de uma vez.

## Passo a passo da instalação

1. **Baixe a versão mais recente:** <https://encurtador.com.br/ZieT>. O link sempre aponta para a última versão publicada. Se ele não abrir (alguns antivírus bloqueiam encurtadores), use o endereço completo: https://github.com/pcmafei/edesk-releases/releases/latest/download/edesk.zip
2. **Crie a pasta** C:\\EDESK (ou o nome escolhido pelo cliente) e **descompacte o zip dentro dela**. Os executáveis devem ficar direto na pasta, não numa subpasta.
3. **Se for uma reinstalação**, feche todos os programas do sistema e copie a pasta atual para um backup antes de descompactar por cima.
4. **Componente de notas (NFe\_Util\_2G):** vai dentro do pacote e é carregado pelo próprio sistema; não há registro manual a fazer.
5. **Crie os atalhos** na Área de Trabalho só para os programas MAFSOFT que o cliente usa (ver Executáveis). Os demais executáveis da pasta não devem ser usados.
6. **Abra o programa principal** (MAFSOFT.exe), entre com CNPJ, usuário e senha e confira a versão no canto da tela de abertura.
7. **Configure o certificado digital:** A1 → selecione o arquivo .pfx e informe a senha; A3 → conecte o token/cartão e selecione-o na lista.
8. **Se o cliente usa o Monitor de notas**, instale-o seguindo a seção Monitor de notas.

## Executáveis do pacote

O pacote traz um executável para cada função. Crie atalho só para os que o cliente usa.

| Executável | Para que serve |
| --- | --- |
| MAFSOFT.exe | Sistema principal (vendas, cadastros, configurações) |
| MAFSOFT\_NFCE.exe | Frente de caixa: emissão de NFC-e |
| MAFSOFT\_PEDIDO.exe | Lançamento de pedidos |
| MAFSOFT\_MONITOR.exe | Monitor de notas (download de NF-e, CT-e, MDF-e e NFS-e) |

## Monitor de notas

O Monitor baixa da SEFAZ todos os documentos destinados ao CNPJ e envia para a nuvem. Ele só trabalha enquanto está aberto, então o lugar onde fica instalado decide se as notas chegam em dia.

- **Instale no servidor ou num computador que fica sempre ligado.** Nunca num notebook ou na máquina de um usuário que desliga à noite.
- **Deixe o Monitor aberto o tempo todo.** Coloque o atalho do MAFSOFT\_MONITOR na pasta Inicializar do Windows (Win+R → shell:startup) para abrir sozinho ao ligar.
- **Um Monitor por CNPJ, em um só computador.** Dois Monitores consultando o mesmo CNPJ fazem a SEFAZ bloquear as consultas por 1 hora. O sistema impede abrir dois na mesma pasta, mas não em computadores diferentes.
- **Não use outro programa de download de notas em paralelo** (FSist, outros sistemas) no mesmo CNPJ, pelo mesmo motivo.
- **Se o Monitor ficar parado,** a MAFSOFT consegue ver pela nuvem há quanto tempo ele está sem trabalhar. Ao reabrir, ele recupera sozinho o que ficou para trás (até 90 dias).

## Atualização automática

A partir da versão 2.85, ninguém precisa mais baixar ou descompactar versões novas. O que o usuário vê:

1. Com o programa aberto, ele verifica a cada 30 minutos se há versão nova e baixa em segundo plano, sem atrapalhar o uso.
2. Com tudo pronto, aparece o aviso **"Atualização disponível"** com as novidades e uma contagem de 60 segundos.
3. **Atualizar agora** (ou deixar a contagem zerar): todos os programas do sistema abertos no computador fecham e **reabrem sozinhos** já atualizados, em menos de um minuto.
4. **Adiar:** o sistema pergunta de novo em 30 minutos. Use durante uma venda ou operação que não pode ser interrompida.

Se algo der errado na versão nova, o sistema volta sozinho para a anterior. A versão instalada aparece na tela de abertura e no título do Monitor.

## Liberações de rede, antivírus e permissões

Em empresas com firewall, proxy ou antivírus corporativo, peça ao TI do cliente para liberar:

| O quê | Por quê |
| --- | --- |
| github.com e objects.githubusercontent.com (HTTPS, porta 443) | Download das atualizações |
| mafsoft.com.br e erp.mafsoft.com.br (HTTPS, porta 443) | Atualização reserva e comunicação com a nuvem |
| Serviços da SEFAZ e do Ambiente Nacional (HTTPS, porta 443) | Emissão e download de documentos fiscais |
| Pasta C:\\EDESK como exceção no antivírus | Evita bloqueio dos programas e da troca de arquivos na atualização |
| PowerShell liberado para o usuário | A atualização usa PowerShell para trocar os arquivos |
| Gravação na pasta C:\\EDESK para os usuários do sistema | Dados locais e atualização |

Para desligar a atualização automática num computador específico (ex.: homologação), crie um arquivo vazio chamado noupdate.flag na pasta do sistema.

## Problemas comuns

| Sintoma | Causa provável | O que fazer |
| --- | --- | --- |
| Aviso "Monitor já em execução" ao abrir | Já há um Monitor aberto nesta pasta (outra janela, bandeja ou outro usuário do servidor) | Use a janela que já está aberta |
| Atualização nunca aparece | Bloqueio de rede, pasta sem gravação, ou noupdate.flag na pasta | Conferir Liberações e o arquivo update.log na pasta |
| Atualização adiada sozinha | Algum usuário clicou em Adiar num dos programas abertos | Normal: o sistema tenta de novo em 30 minutos |
| Versão voltou para a anterior | A versão nova não abriu em 2 minutos e o sistema desfez a troca | Avisar o suporte com o arquivo update.log |
| Notas de compra não aparecem na nuvem | Monitor fechado ou computador desligado | Abrir o Monitor; ele recupera o atraso sozinho |
| Monitor mostra "aguardando SEFAZ" | Consumo indevido: outro programa consultou o mesmo CNPJ | Aguardar 1 hora e remover o outro programa de download |
| Erro de certificado | Certificado vencido, senha errada ou token desconectado | Reconfigurar o certificado nas Configurações |

Suporte MAFSOFT: WhatsApp/telefone (43) 99130-0342.

## Checklist do representante

Marque cada item ao final da instalação no cliente:

- [ ] Pasta C:\\EDESK (ou nome escolhido) criada fora de Arquivos de Programas, Desktop e OneDrive
- [ ] Versão mais recente baixada do link oficial e descompactada direto na pasta
- [ ] Backup da pasta antiga feito (em reinstalação)
- [ ] Atalhos criados só para os programas que o cliente usa
- [ ] Login feito e versão conferida na tela de abertura
- [ ] Certificado digital configurado e testado
- [ ] Monitor instalado em computador sempre ligado, com atalho na Inicialização do Windows
- [ ] Nenhum outro programa de download de notas ativo no mesmo CNPJ
- [ ] Liberações de rede e antivírus confirmadas com o TI do cliente
- [ ] Cliente orientado sobre o aviso de atualização (Atualizar agora ou Adiar)

## Histórico de versões

| Versão | Data | Alteração |
| --- | --- | --- |
| 1.0 | 14/10/2026 | Primeira versão publicada |
