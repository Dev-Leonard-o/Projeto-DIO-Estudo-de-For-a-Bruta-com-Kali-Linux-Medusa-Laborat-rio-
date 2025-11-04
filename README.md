# Projeto DIO estudo de força bruta com kali-linux + enumeração + medusa + enum4linux (Laboratório Controlado)

<br>
<br>
<h1> Introdução </h1>
  <p> 
  Em um cenário de cibersegurança, a compreensão das táticas ofensivas é fundamental para a construção de defesas robustas. Este relatório detalha um <strong>projeto</strong> de estudo focado na simulação de um ataque de <strong>força bruta</strong>, uma técnica que     explora a repetição sistemática para quebrar credenciais de acesso. A iniciativa foi realizada em um <strong>laboratório controlado e ético</strong>, garantindo um ambiente seguro para a experimentação, o projeto faz parte do Bootcamp da Digital Innovation One (DIO).

  A simulação empregou o sistema operacional **Kali Linux**, uma distribuição especializada em testes de penetração, e a ferramenta **Medusa** para automatizar e executar os ataques de força bruta. Para enriquecer a fase de reconhecimento, o projeto também utilizou técnicas de **enumeração** e as ferramentas: <strong>Nmap</strong>, **enum4linux**, que são cruciais para coletar informações valiosas sobre os sistemas e usuários-alvo antes do ataque propriamente dito. Assim como a criação de wordlists para obter um melhor desempenho das ferramentas. Este exercício prático teve como objetivo principal demonstrar a eficácia dessas ferramentas e a importância crítica de políticas de senha fortes e monitoramento contínuo da rede. </p>

<br>

<h2> Índice </h2>

  <ol>
    <li> Objetivos</li>
    <li> Aviso de Ética e Uso </li>
    <li> Ambiente (infra)</li>
    <li> Cenários Testados </li>
            <ul>
               <li> FTP (Força bruta com Medusa)</li>
               <li> Enumeração em Web Forms (DVWA)</li>
               <li> SMB (password spraying + enumeração)</li>
            </ul>
    </li>
    <li> Wordlists utlizadas</li>
    <li> Comandos (exemplos) </li>
    <li> Experimento SSH: Invasão a máquina via conexão SSH
             <ul>
               <li> "Unable to negotiate", Causa e solução</li>
               <li> Conexão não autorizada a máquina via SSH</li>
               <li> Criação de um arquivo .txt "Hello World" remoto</li>
             </ul>
    </li>
    <li> Evidências e validação </li>
    <li> Recomendações de mitigação</li>
    <li> Estrutura do repositório</li>
    <li> Referências e materiais de estudo</li>
  </ol>

<br>

<h3>1. Objetivos</h3>
  <ul>
    <li> Demonstrar ataques de força bruta em </li>
    <li> Praticar uso das ferramentas <strong>nmap</strong>, <strong>Medusa</strong> <strong>Enum4linux</strong></li>
    <li> Gerar Documentação técnica clara e objetiva, com comandos, wordlists, e sugestões de mitigação</li>
    <li> Registrar uma atividade extra como experimento adicional realizado via SSH(Invasão, navegação e criação de arquivo hello_world.txt, assim como registrar um problema comum observado (Unable to negotiate).</li>
    <li> Aprender a validar resultados e gerar evidências para um relatório técnico profissional</li>
  </ul>

  <br>

  
<h3>2. Aviso de Ética e Uso</h3>
  <ul>
    <li> Todos os testes foram realizados em <strong>ambiente isolado</strong> (VMs locais) e autorizados (Ambiente com fins educacionais) </li>
    <li> É expressamente <strong>PROIBIDO</strong> executar testes fora de ambientes controlados e autorizados</li>
    <li>A finalidade deste projeto tem cunho educativo, tal qual é: entender vulnerabilidades e propor contramedidas.</li>
  </ul>

  <br>

 <h3>3. Ambiente (Infra)</h3>
  <ul>
    <li>Virtual box com duas VM'S em <strong> host-only / internal network</strong>, sendo: 
        <ul>
          <li><strong>Kali Linux</strong> (atacante) - Ferramentas instaladas (Medusa, enum4linux, nmap) /li>
          <li><strong>Metasploitable 2</strong>(alvo vulnerável) - Serviços: FTP (vsftpd), SMB (Samba), HTTP (DVWA instalado/servindo).</li>
        </ul>
    </li>
     <li> Endereços IPs de exemplo (rede host-only):
          <ul>
            <li> Kali: <strong>192.168.56.102</strong></li>
            <li> Metasploitable: <strong>192.168.56.101</strong></li>
          </ul>
     </li>
  </ul>
 
 <br>
 
 <h3>4. Cenários testados</h3>
     <h4> &nbsp &nbsp &nbsp &nbsp Cenário A → FTP (Força bruta)</h4>
