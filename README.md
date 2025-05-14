# Desafio DIO: Criando uma Máquina Virtual no Azure e Documentando o Processo



![Screenshot from 2025-05-13 23-27-01](https://github.com/user-attachments/assets/784b852f-1bcf-4063-a04c-9a178a79938f)


## Introdução

Este repositório documenta o processo de criação e configuração de uma máquina virtual (VM) na plataforma Microsoft Azure, como parte de um desafio proposto pela Digital Innovation One (DIO). O objetivo é aplicar os conhecimentos adquiridos sobre computação em nuvem com Azure e praticar a documentação técnica utilizando Git e GitHub.

## Objetivo deste Repositório

Este repositório serve como um guia prático e material de consulta, contendo:
*   Um passo a passo detalhado da criação de uma VM no Azure.
*   Anotações e dicas relevantes sobre o uso da plataforma Azure.
*   Recursos úteis para estudos e futuras implementações.

---

## Passo a Passo: Criando uma Máquina Virtual no Portal do Azure

A seguir, detalhamos as etapas para criar uma máquina virtual (VM) utilizando o Portal do Azure.

### 1. Acesso ao Portal do Azure
   *   Acesse o [Portal do Azure](https://portal.azure.com).
   *   Faça login com suas credenciais da conta Azure.

### 2. Criar um Novo Recurso
   *   No canto superior esquerdo, clique em **"+ Criar um recurso"**.
   *   Na barra de busca do Azure Marketplace, procure por **"Máquina Virtual"**.
   *   Selecione "Máquina Virtual" nos resultados e clique em **"Criar"**.

### 3. Configurações da Guia "Básico"

   *   **Assinatura**: Selecione sua assinatura do Azure.
   *   **Grupo de Recursos**:
        *   Essencial para organizar todos os recursos relacionados à sua VM.
        *   Selecione um existente ou clique em **"Criar novo"** (Recomendado: `meu-grupo-vm-desafio-dio`).
   *   **Nome da máquina virtual**: Escolha um nome único (Ex: `minha-vm-windows` ou `minha-vm-ubuntu`).
   *   **Região**: Selecione a região geográfica mais adequada (Ex: `Brazil South`, `East US`).
   *   **Opções de disponibilidade**: Para este desafio, "Nenhuma redundância de infraestrutura necessária" geralmente é suficiente.
   *   **Tipo de segurança**: Pode manter o padrão "Standard" ou explorar outras opções se necessário.
   *   **Imagem**: Selecione o sistema operacional para sua VM.
        *   Exemplos populares: `Ubuntu Server LTS`, `Windows Server Datacenter`.
        *   Clique em "Ver todas as imagens" para mais opções.
   *   **Tamanho da VM**: Define CPU, RAM e, consequentemente, o custo.
        *   Clique em "Alterar tamanho" para ver as opções.
        *   Para aprendizado, tamanhos menores como da série `B` (Ex: `Standard_B1s`) são mais econômicos.
   *   **Conta de administrador**:
        *   **Tipo de autenticação**:
            *   **Linux**: "Chave pública SSH" (recomendado) ou "Senha".
                *   Se SSH, você pode gerar um novo par de chaves ou usar uma existente. **Guarde bem a chave privada se gerar uma nova!**
            *   **Windows**: "Senha".
        *   **Nome de usuário**: Defina o nome do usuário administrador (Ex: `azureuser` para Linux, `adminvm` para Windows).
        *   **Senha / Chave pública SSH**: Forneça as credenciais conforme o tipo de autenticação escolhido.
   *   **Regras de porta de entrada / Portas de entrada públicas**:
        *   Permite o acesso à VM.
        *   Selecione "Permitir portas selecionadas".
        *   **Linux**: Marque **SSH (22)**.
        *   **Windows**: Marque **RDP (3389)**.

### 4. Configurações da Guia "Discos"

   *   **Tipo de disco do SO**:
        *   Opções: SSD Premium, SSD Standard, HDD Standard.
        *   `SSD Standard` oferece um bom equilíbrio entre performance e custo para muitos cenários.
   *   **Gerenciamento de chaves**: Pode manter o padrão "Chave gerenciada pela plataforma".
   *   *Opcional*: Adicionar discos de dados, se necessário.

### 5. Configurações da Guia "Rede"

   *   **Rede virtual**: Geralmente, uma nova VNet é criada automaticamente. Pode aceitar os padrões.
   *   **Sub-rede**: Criada automaticamente dentro da VNet.
   *   **IP público**: Um novo IP público será criado para permitir o acesso à VM pela internet.
   *   **NSG (Grupo de Segurança de Rede) da NIC**: Selecione "Básico". As regras de porta definidas na guia "Básico" serão aplicadas aqui.
   *   **Balanceamento de carga**: Selecione "Nenhum" para este desafio.

### 6. Configurações da Guia "Gerenciamento"

   *   Explore opções como monitoramento, identidade, desligamento automático (útil para economizar custos).
   *   Para este desafio, os padrões costumam ser suficientes. Considere configurar o **Desligamento automático** para evitar cobranças inesperadas.

### 7. Configurações da Guia "Avançado"
   *   Geralmente não requer alterações para uma VM básica.

### 8. Configurações da Guia "Marcas"
   *   Adicione marcas (tags) para organizar e identificar seus recursos.
        *   Exemplo: `Nome: Projeto, Valor: DesafioDIO`
        *   Exemplo: `Nome: Ambiente, Valor: Estudo`

### 9. Revisar + criar
   *   O Azure validará suas configurações. Corrija quaisquer erros indicados.
   *   Revise cuidadosamente o resumo, especialmente o **tamanho da VM** e o **custo estimado**.
   *   Clique em **"Criar"**.

### 10. Implantação
    *   Aguarde alguns minutos enquanto o Azure provisiona sua VM.
    *   **Importante (para Linux com SSH)**: Se você optou por gerar um novo par de chaves SSH, o Azure solicitará o download da chave privada (arquivo `.pem`). **Baixe este arquivo imediatamente e guarde-o em um local seguro.** Você não poderá baixá-lo novamente.

---

## Conectando à Máquina Virtual

Após a VM ser criada e estar em execução ("Running"):

1.  No Portal do Azure, navegue até sua máquina virtual.
2.  Na página de "Visão Geral", localize o **Endereço IP Público**.
3.  Clique no botão **"Conectar"** para ver as instruções específicas.

### Para VMs Linux (usando SSH):
   *   Você precisará de um cliente SSH (Terminal no Linux/macOS, PuTTY ou WSL/Windows Terminal no Windows).
   *   Comando exemplo (se estiver usando chave SSH):
     ```bash
     ssh -i /caminho/para/sua/chave_privada.pem nome_de_usuario@SEU_ENDERECO_IP_PUBLICO
     ```
   *   Se estiver usando senha, o comando será mais simples, e a senha será solicitada:
     ```bash
     ssh nome_de_usuario@SEU_ENDERECO_IP_PUBLICO
     ```

### Para VMs Windows (usando RDP - Remote Desktop Protocol):
   *   Clique em "Baixar Arquivo RDP" na seção "Conectar" da VM no portal.
   *   Abra o arquivo `.rdp` baixado.
   *   Use o nome de usuário e senha que você configurou durante a criação da VM.

---

## Dicas Importantes e Boas Práticas

*   **Gerenciamento de Custos**:
    *   Sempre desligue (`Stop (Deallocate)`) sua VM quando não estiver em uso para evitar cobranças desnecessárias. VMs paradas (desalocadas) não incorrem em custos de computação, apenas de armazenamento.
    *   Exclua o **Grupo de Recursos** quando o projeto/estudo for concluído para remover todos os recursos associados de uma vez.
*   **Segurança**:
    *   Use senhas fortes ou, preferencialmente, autenticação por chave SSH para VMs Linux.
    *   Não exponha mais portas do que o necessário. Use Grupos de Segurança de Rede (NSG) para controlar o tráfego de entrada e saída.
*   **Organização**:
    *   Utilize Grupos de Recursos para agrupar todos os componentes da sua solução.
    *   Use Marcas (Tags) para categorizar e gerenciar seus recursos.

---

## Minhas Anotações e Aprendizados

*(Esta seção é para você preencher!)*

*   Descreva aqui quaisquer desafios que você enfrentou.
*   Quais foram os conceitos mais importantes que você aprendeu ou reforçou?
*   Dicas específicas que você descobriu durante o processo.
*   Como a criação desta VM se relaciona com projetos futuros ou estudos?
*   *Opcional: Adicione links para suas capturas de tela (ex: `[Veja a configuração de rede](./images/config-rede.png)`)*

---

## Recursos Úteis

*   **Documentação Oficial do Azure**:
    *   [Início Rápido: Criar uma máquina virtual do Windows no Portal do Azure](https://learn.microsoft.com/pt-br/azure/virtual-machines/windows/quick-create-portal)
    *   [Início Rápido: Criar uma máquina virtual do Linux no Portal do Azure](https://learn.microsoft.com/pt-br/azure/virtual-machines/linux/quick-create-portal)
*   **Materiais Complementares sobre GitHub**:
    *   [GitHub Quick Start](https://github.com/digitalinnovationone/dio-lab-open-source/blob/main/QUICKSTART.md)
    *   [GitBook: Formação GitHub Certification](https://www.gitbook.com/book/digitalinnovationone/git-e-github-para-iniciantes/details)
    *   [Documentação do GitHub](https://docs.github.com/)
    *   [GitHub Markdown Guide](https://guides.github.com/features/mastering-markdown/)

---

Este projeto foi desenvolvido como parte do bootcamp da [Digital Innovation One (DIO)](https://www.dio.me/).
