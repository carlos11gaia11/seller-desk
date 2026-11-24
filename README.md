# Seller Desk Portable

Personalização do RustDesk para facilitar o suporte remoto: preto e laranja,
código em destaque, botão de copiar, tutorial em português e assinatura
“Aplicativo Modificado por Carlos Gaia” no rodapé da janela principal.
O ícone tem fundo preto e a letra S em laranja.

## Compilar

Abra **Actions → Seller Desk Portable Windows → Run workflow**.
O fluxo também executa quando a configuração, as personalizações ou o ícone
são enviados para `main`. Ao concluir, baixe o artefato
`SellerDesk-Portable-Windows-x64` e extraia `SellerDesk-Portable.exe`.
Esse é o arquivo a enviar para quem precisa de suporte; não é necessário
enviar o projeto, Flutter, DLLs separadas ou instalar o aplicativo.

O primeiro build pode demorar, pois compila Rust, Flutter e bibliotecas nativas.
O executável ainda precisa ser validado em uma sessão real de suporte remoto.
O fluxo não publica releases nem usa credenciais de assinatura digital.

## Como funciona o portátil

Usa o empacotador original do RustDesk. As bibliotecas e recursos ficam
embutidos no executável e são extraídos automaticamente em uma pasta de
dados do usuário ao abrir. Configurações podem permanecer no computador.
Não é um executável que roda exclusivamente na memória.

O nome `SellerDesk-Portable.exe` não termina em `install.exe`, portanto não
aciona o modo instalador do empacotador. O uso normal continua exigindo
consentimento ou senha, conforme a configuração do aplicativo.

## Código-fonte reproduzível

A base foi identificada no comentário do ZIP original e verificada no GitHub:
`rustdesk/rustdesk@51f94394ce61e1f3d26229565c326b2862cbdd1f`.
O workflow faz checkout dessa revisão e de seus submódulos, aplica
`patches/seller-desk.patch` e copia `assets/seller-desk.ico` para os dois
recursos de ícone do Windows. O patch foi verificado contra o ZIP original.

Para reconstruir manualmente, faça checkout dessa revisão com seus submódulos,
aplique o patch e copie o ícone para `res/icon.ico` e
`flutter/windows/runner/resources/app_icon.ico`. Siga os passos do workflow
incluído para preparar dependências, gerar bridges, compilar e empacotar.

## Escopo das alterações

- `desktop_home_page.dart`: painel de recebimento, ID e layout responsivo.
- `seller_desk.dart`: componentes de marca, código, cópia e tutorial.
- `desktop_tab_page.dart`: assinatura fixa, discreta, no rodapé principal.
- `tabbar_widget.dart`: nome e S da marca na barra da janela.
- `common.dart`: paleta, tema inicial, títulos e altura do rodapé no modo de recebimento.
- `Runner.rc` e `libs/portable/Cargo.toml`: metadados Windows da marca.
- Dois ícones Windows: mesma marca no executável interno e no empacotador.

Protocolo, autenticação e servidores não foram alterados. Identificadores
internos do RustDesk permanecem para preservar integração e compatibilidade.
O ícone da bandeja e outras plataformas não foram redesenhados.
Drivers opcionais de impressora e monitor virtual não são adicionados pelo
fluxo portátil; o foco é suporte remoto básico em Windows x64.

## Licença

Baseado em RustDesk, licenciado sob AGPL-3.0. A licença original está em
`LICENSE`. Os avisos e créditos do código original permanecem preservados.
Este repositório contém as alterações e a referência exata para reconstruir
o código-fonte correspondente. Personalização por Carlos Gaia.
