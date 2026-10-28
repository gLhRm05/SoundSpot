# SoundSpot

Widget de música para Windows com reprodução local pelo Spotify Soloist, pesquisa, playlists, fila editável e temas personalizáveis.

## Download

[Baixar SoundSpot 1.11.1 para Windows](https://github.com/gLhRm05/SoundSpot/releases/download/v1.11.1/SoundSpot-1.11.1-Windows.exe)

[Ver todas as versões](https://github.com/gLhRm05/SoundSpot/releases)

Baixe o executável na seção **Assets** da Release. O Soloist é obtido separadamente pelo site oficial; cada usuário configura sua própria conta.

Para atualizar, encerre o widget pelo ícone da bandeja → **Sair** antes de abrir a nova versão.

## Tutorial de configuração e primeiro uso

Siga estas etapas mesmo que já tenha recebido os executáveis. Para usar busca, playlists e reprodução, é necessário configurar **o áudio pelo Soloist** e **a biblioteca pela conta Spotify**.

### 1. Preparar os arquivos

Você precisa de Windows 10/11 de 64 bits, conexão com a internet, sua conta Spotify Premium e o Spotify no celular para o primeiro pareamento. Nessa primeira conexão, o celular e o computador devem estar na mesma rede local.

1. Crie uma pasta permanente, por exemplo `Documentos\SoundSpot`.
2. Coloque nela o executável `SoundSpot-1.11.1-Windows.exe`.
3. Guarde o arquivo oficial `soloist.exe` em uma subpasta, por exemplo `Documentos\SoundSpot\Soloist`. Se recebeu um ZIP, extraia os arquivos antes de continuar. Se ainda não tem o Soloist, obtenha a versão Windows x86_64 nos [downloads oficiais](https://developer.spotify.com/documentation/soloist/reference/downloads-and-updates).
4. Abra o executável do SoundSpot com dois cliques.

O SoundSpot é portátil: não há um instalador tradicional e você não precisa instalar Node.js ou Electron para utilizá-lo. O Soloist é um componente separado e não vem dentro do pacote do widget.

### 2. Entender as duas credenciais

| Informação               | Para que serve                            | Quem fornece                                                           |
| ------------------------ | ----------------------------------------- | ---------------------------------------------------------------------- |
| Chave pessoal do Soloist | Reproduzir áudio e controlar o player     | Cada usuário gera a própria chave                                      |
| Client ID do Spotify     | Pesquisar e carregar playlists e curtidas | Pode ser fornecido pelo responsável pelo aplicativo ou criado por você |

A chave Soloist e o Client ID são diferentes. Use sua própria conta Spotify nas duas conexões. O widget não solicita Client Secret nem a senha de outra pessoa.

### 3. Configurar o reprodutor Soloist

1. Entre com sua conta em [Spotify Soloist API Key](https://developer.spotify.com/dashboard/soloist) e gere sua chave pessoal. A geração exige Premium; cada pessoa deve gerar a própria chave, sem compartilhá-la.
2. No SoundSpot, clique na **engrenagem → Reprodutor**.
3. Clique em **Selecionar…** e escolha o arquivo `soloist.exe` extraído na etapa 1. A localização `%LOCALAPPDATA%\SoundSpot\Soloist\soloist.exe` também é reconhecida automaticamente.
4. Cole a chave no campo **Sua chave pessoal do Soloist**.
5. Mantenha o nome padrão do dispositivo ou escolha outro e clique em **Salvar e iniciar**.

O widget inicia o Soloist por você; não é necessário abrir `soloist.exe` manualmente. A chave fica protegida pelo Windows e deixa de aparecer no formulário depois de salva. Em configurações futuras, deixe o campo vazio para manter a chave já cadastrada.

### 4. Fazer o primeiro pareamento

1. Mantenha o reprodutor iniciado pelo SoundSpot. Se aparecer **Aguardando pareamento…**, abra o Spotify no celular.
2. No celular, entre na mesma conta que usará na biblioteca do widget e abra a tela de uma música.
3. Abra **Dispositivos** ou **Conectar a um dispositivo**.
4. Selecione **SoundSpot — Soloist**, ou o nome que você definiu na etapa anterior.
5. Inicie uma música, se necessário, e aguarde o status **Pronto** na aba Reprodutor do SoundSpot.

O pareamento é restaurado nas próximas inicializações. Depois de concluir também a conexão da biblioteca, o Spotify de desktop pode ficar fechado durante o uso do widget.

Para trocar a conta do áudio, use **Reprodutor → Apagar pareamento e parear novamente** e repita esta etapa. **Parar** encerra o processo de áudio.

### 5. Conectar a biblioteca Spotify

**Se recebeu um Client ID:** peça ao responsável pelo aplicativo que autorize sua conta em **Settings → Users Management** no [Spotify Developer Dashboard](https://developer.spotify.com/dashboard). Ele também deve cadastrar o endereço de retorno abaixo. Você fará o login com sua própria conta.

**Se vai criar seu próprio Client ID:** entre no [Spotify Developer Dashboard](https://developer.spotify.com/dashboard), crie um aplicativo para a **Web API** e abra suas configurações. Cadastre este **Redirect URI**, exatamente como está escrito, e salve:

```text
http://127.0.0.1:43821/callback
```

Copie o **Client ID** do aplicativo. Não copie o Client Secret. O aplicativo e os usuários autorizados precisam atender às [regras do modo de desenvolvimento da Web API](https://developer.spotify.com/documentation/web-api/concepts/quota-modes).

Agora finalize no widget:

1. Abra **engrenagem → Conta Spotify**.
2. Cole o Client ID no campo correspondente. O botão **Copiar endereço** fornece o Redirect URI para cadastrar no Dashboard.
3. Clique em **Conectar** e, no navegador, autorize usando a **mesma conta do pareamento Soloist**.
4. Volte ao SoundSpot e confira o nome da conta conectada na aba Conta Spotify.

O navegador é usado para essa autorização inicial. O OAuth solicita leitura de playlists e biblioteca, sem escopos de controle remoto do player. O protocolo Soloist não fornece um ID de usuário para comparar automaticamente as duas contas; confira se usou a mesma conta em ambas.

### 6. Testar e começar a usar

1. Feche o painel de configurações e pesquise uma música ou artista na barra de busca.
2. Clique em uma faixa e confira se título, progresso e áudio acompanham a reprodução.
3. Para ouvir uma coleção, abra **Minhas playlists**, escolha uma playlist ou **Minhas curtidas** e use **Reproduzir tudo** ou selecione uma faixa.
4. Use **+** ao lado de uma música para adicioná-la à fila. Abra **Fila** para consultar as próximas, arrastar músicas para mudar a ordem, remover pelo **X** ou usar **Limpar fila**, mantendo a música atual.

Se houver um erro, consulte [Quando algo não funcionar](#quando-algo-não-funcionar). O áudio depende de internet; o widget não funciona como reprodutor offline.

### 7. Personalizar e abrir com o Windows

Em **engrenagem → Aparência**, escolha o tema, ajuste as cores no modo Personalizado, mostre ou oculte a capa e abra **Tamanho do widget** para ajustar a escala. As preferências ficam salvas automaticamente.

Para abrir o widget ao entrar na sua conta do Windows, ative **Iniciar ao ligar**. Mantenha o executável portátil na pasta permanente escolhida. Para cancelar essa inicialização, desative a mesma opção.

Nas próximas vezes, basta abrir o SoundSpot. O **X** da janela apenas oculta o widget na bandeja, perto do relógio; clique no ícone para voltar. Para encerrar de verdade, use **botão direito no ícone da bandeja → Sair**. Ao atualizar a versão, encerre a anterior dessa forma antes de abrir o novo executável.

### Atualizar o Soloist quando necessário

As builds Soloist expiram 90 dias após a compilação. Se a aba Reprodutor informar que a versão expirou, obtenha uma build atual nos [downloads oficiais](https://developer.spotify.com/documentation/soloist/reference/downloads-and-updates) e selecione o novo `soloist.exe`. Consulte também a [autenticação oficial do Soloist](https://developer.spotify.com/documentation/soloist/concepts/authentication).

## Quando algo não funcionar

- **Reprodutor indisponível:** abra Configurações → Reprodutor, confira executável/chave e faça o pareamento inicial pelo celular.
- **Redirect inválido:** confira o endereço completo, incluindo porta e `/callback`. O Spotify não aceita `localhost` nessa configuração.
- **403 / comando recusado:** confira Premium, usuários autorizados e reconecte a conta para renovar as permissões.
- **429:** aguarde a pausa indicada. As cotas do Spotify são compartilhadas pelos aplicativos de um mesmo desenvolvedor.
- **Porta ocupada:** encerre outra instância que esteja usando a porta 43821 e tente novamente.

O projeto é independente e não é um produto oficial do Spotify. A validação automatizada usa respostas controladas; a autenticação e a reprodução reais dependem da configuração e autorização da sua conta.
