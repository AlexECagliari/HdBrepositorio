# HdBrepositorio
<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8">
  <title>Explicação do Diagrama de Rede</title>
  <style>
    body { font-family: Arial, sans-serif; line-height: 1.6; margin: 20px; }
    pre { background: #f4f4f4; padding: 10px; border: 1px solid #ddd; overflow-x: auto; }
    h1, h2 { color: #333; }
    code { background: #eef; padding: 2px 4px; border-radius: 3px; }
  </style>
</head>
<body>
  <h1>Diagrama de Rede Atualizado</h1>
  
  <p>A seguir, encontra-se o diagrama visual representado em <code>Mermaid</code>, que incorpora as conexões <strong>VPN site-to-site</strong>, <strong>VPN client-to-site</strong> e a representação da infraestrutura na nuvem pública (AWS).</p>
  
  <h2>Código do Diagrama (Mermaid)</h2>
  <pre>
flowchart TD
    %% Bloco de Conexões Externas e DMZ
    Internet[Internet]
    FirewallExt[Firewall Externo]
    DMZ[DMZ<br/>(Servidor Web, Servidor Email,<br/>Firewall Interno)]
    
    %% Bloco da Rede Interna (Sede)
    Intranet[Intranet da Empresa<br/>(Servidores, Workstations)]
    
    %% Dispositivos VPN para Site-to-Site
    RouterSede[Dispositivo VPN (Sede)]
    RouterFilial[Dispositivo VPN (Filial)]
    
    %% Bloco da Filial
    Filial[Filial da Empresa<br/>(Rede Local)]
    
    %% Representação da Nuvem Pública (AWS)
    AWS[AWS (Cloud Pública)<br/>(Instâncias de Servidores)]
    
    %% Dispositivos para VPN Client-to-Site (Home Office)
    HomeVPN[Funcionários Home Office<br/>(VPN Client)]
    
    %% Conexões principais
    Internet --> FirewallExt
    FirewallExt --> DMZ
    DMZ --> Intranet

    %% VPN Client-to-Site: Funcionários conectam de casa, passando pelo Firewall Externo até a DMZ
    HomeVPN --- FirewallExt

    %% VPN Site-to-Site: conexão segura entre a Sede e a Filial, passando pelos dispositivos VPN
    Intranet --- RouterSede
    RouterSede -- "VPN Tunnel" -- RouterFilial
    RouterFilial --- Filial

    %% Conexão entre a DMZ e a infraestrutura na AWS
    DMZ --- AWS
  </pre>
  
  <h2>Explicação do Diagrama</h2>
  <ul>
    <li>
      <strong>Internet → Firewall Externo → DMZ:</strong>
      <p>O tráfego vindo da Internet é filtrado pelo <em>Firewall Externo</em> e direcionado para a <em>DMZ</em>, onde encontram-se os servidores expostos (Servidor Web e Servidor Email) e o <em>Firewall Interno</em> que segmenta a rede.</p>
    </li>
    <li>
      <strong>DMZ → Intranet:</strong>
      <p>Após a DMZ, o tráfego autorizado é encaminhado para a <em>Intranet da Empresa</em>, que abriga servidores, workstations e outros recursos internos.</p>
    </li>
    <li>
      <strong>VPN Client-to-Site:</strong>
      <p>Os funcionários que trabalham em <em>Home Office</em> se conectam à rede interna utilizando clientes VPN. Essa conexão passa pelo <em>Firewall Externo</em> e alcança a DMZ, de onde o acesso é direcionado à Intranet.</p>
    </li>
    <li>
      <strong>VPN Site-to-Site:</strong>
      <p>Para garantir uma comunicação segura entre a sede e a filial, a conexão VPN site-to-site é estabelecida por meio de dispositivos VPN instalados em ambos os lados (Sede e Filial). Essa conexão passa pelos respectivos firewalls e cria um túnel VPN seguro.</p>
    </li>
    <li>
      <strong>Conexão com a AWS (Cloud Pública):</strong>
      <p>A infraestrutura na nuvem pública, representada pela <em>AWS</em>, possui instâncias de servidores que se conectam à DMZ, possibilitando a integração dos recursos da nuvem com a rede interna da empresa.</p>
    </li>
  </ul>
  
  <p>Este diagrama ilustra de forma clara a segmentação de rede e as diversas conexões VPN utilizadas para garantir a segurança e o acesso remoto à rede corporativa.</p>
  
  <p>Você pode copiar e colar o código do diagrama em um editor compatível com <code>Mermaid</code> (como o <a href="https://mermaid.live" target="_blank">Mermaid Live Editor</a>) para visualizá-lo e realizar eventuais ajustes conforme a necessidade da sua infraestrutura.</p>
</body>
</html>
