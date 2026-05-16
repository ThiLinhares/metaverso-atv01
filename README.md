# Projeto Final: Meu Primeiro Ambiente VR 🏕️⚒️

<p align="center">
  <a href="https://unity.com/"><img src="https://img.shields.io/badge/Unity-6-black.svg?logo=unity" alt="Unity Version"></a>
  <img src="https://img.shields.io/badge/Render_Pipeline-URP-2f855a.svg" alt="URP">
  <img src="https://img.shields.io/badge/Target-Meta%20Quest%20(Android)-1c1e21.svg" alt="Target">
  <img src="https://img.shields.io/badge/Status-Concluído-success.svg" alt="Status">
</p>

---

## 1. INFORMAÇÕES DO ESTUDANTE
- **Nome Completo:** Thiago Linhares
- **Curso:** Residência em TIC 29 - Web 3.0
---

## 2. RESUMO DO PROJETO E CONTEXTO XR
Este projeto consubstancia a entrega do "Primeiro Ambiente VR", propondo um cenário tridimensional interativo com a temática de um **Acampamento**. Adotando uma direção de arte *Low Poly* (inspirada na estética de MMORPGs clássicos), o ambiente foi meticulosamente planejado para proporcionar imersão espacial e navegação fluida.

Os elementos foram dispostos em um layout de acampamento em clareira, garantindo o reconhecimento imediato dos pontos de interesse e mantendo a coerência visual e escala espacial, fatores indispensáveis para experiências XR focadas em presença virtual.

---

## 3. CONFIGURAÇÃO TÉCNICA E VALIDAÇÃO DE REQUISITOS 

O ecossistema do projeto foi configurado com rigor técnico, visando performance e compatibilidade nativa com os modernos *headsets* Standalone.

| Requisito Técnico | Descrição da Implementação |
| :--- | :--- |
| **Engine & Render Pipeline** | Desenvolvido no **Unity 6** utilizando a **Universal Render Pipeline (URP)** para o balanço ideal entre fidelidade visual e otimização em plataformas móveis. |
| **Integração de SDK** | **Meta XR SDK** importado e devidamente mapeado no ecossistema da aplicação. |
| **Build Target** | Plataforma configurada para **Android**, visando o *deploy* otimizado em dispositivos da família Meta Quest. |
| **XR Setup** | **XR Plugin Management** inicializado e rodando sob o provedor *OpenXR*. |
| **Sistema de Input/Navegação** | Hibridismo na locomoção: Implementação central através do componente **First Person Controller** conectado ao *New Input System*. O projeto pode ser navegado integralmente via PC (teclado/mouse), agilizando testes lógicos e mecânicos sem dependência exclusiva dos óculos VR a cada iteração no Editor. |

---

## 4. MAPEAMENTO DE ELEMENTOS DO AMBIENTE VIRTUAL 

O cenário é composto por ativos 3D distribuídos cenograficamente para formar a atmosfera da forja ao ar livre:

- **Terreno/Piso:** Plano principal texturizado em material orgânico (grama), contendo o sistema de colisores de física (Mesh/Box Colliders) responsável por restringir a navegação do usuário estritamente na área jogável e limitar fugas de cenário.
- **Atmosfera (Skybox):** Sistema celestial gerido pelo *Fantasy Skybox FREE*, projetando a base tonal do cenário e envelopando o usuário em um domo verossímil e iluminado.
- **Catálogo de Assets 3D Importados:** No mínimo 5 componentes centrais definem a identidade do mapa:
  1. `Tenda` (Abrigo central estrutural do local)
  2. `Fogueira_Principal` (Ponto de convergência e claridade)
  3. `Mesa_Trabalho` (Apoio logístico para materiais)
  4. `Barris_Suprimentos` (Props de composição e oclusão de cenário em segundo plano)

---

## 5. ARQUITETURA DA HIERARQUIA E QUALIDADE DE CÓDIGO

A cena foi estruturada empregando *Clean Architecture* e *Separation of Concerns*, mantendo a janela *Hierarchy* perfeitamente modular e o repositório completamente limpo de arquivos redundantes ou temporários (*dead files*). 

A árvore de objetos está agrupada de forma lógica e autoexplicativa através de *parent containers*:
```text
▼ SampleScene
  ├── ── GERENCIADORES ──
  ├── ── ILUMINAÇÃO & SETUP ──
  ├── Ambiente_acampamento
  │   ├── Terreno_e_Agua
  │   ├── Vegetacao_e_rochas
  │   ├── Props_Acampamento
  │   └── Barreiras_Invisiveis
  └── PlayerCapsule
```
*A consistência da nomenclatura garante manutenibilidade ágil, isolando a iluminação, gerênciadores e a infraestrutura ambiental do jogador de maneira profissional.*

---

## 6. PROCESSO DE CRIAÇÃO, REFLEXÃO E ANÁLISE DE SOLUÇÕES 

Durante a esteira de produção e o *level design*, foram superados importantes obstáculos técnicos. Seguem as principais resoluções:

### 6.1 Correção Fotométrica e Setup de Iluminação
**Problema:** O *Skybox* provocava um vazamento massivo da cor azul nas sombras (*Blue Tint*), quebrando completamente a atmosfera calorosa esperada em um acampamento terrestre.  
**Solução:** Alterou-se o parâmetro `Environment Lighting (Source)` nativo de "Skybox" para "Color", definindo uma cor base neutra com intensidade reduzida para `0.5`. O *Main Sun* (`Directional Light`) recebeu um tom quente e ajustamos a intensidade luminosa direcional para `2.0`, trazendo contraste harmonioso e calibrado.

### 6.2 Otimização de Física na Locomoção
**Problema:** O controle *First Person Controller* permitia que o usuário desferisse saltos irreais durante os testes, quebrando a imersão de XR e aumentando a vertigem (*motion sickness*).  
**Solução:** O pulo foi anulado zerando a variável `Jump Height` do Character Controller, ancorando o usuário com gravidade real e mantendo o treinamento puramente terrestre:
```csharp
// Script adaptado: FirstPersonController.cs
[Tooltip("The height the player can jump")]
public float JumpHeight = 0.0f; // Pulo fixado em 0 para locomoção VR controlada
```

### 6.3 Resolução de Conflitos e Manipulação de Histórico do Git
**Problema 1 (Históricos Desvinculados):** O versionamento inicial resultou em bifurcações. Ao sincronizar com o Remote, o GitHub negou a integração: `[rejected] main -> main (fetch first)`.  
**Solução 1:** Unificação forçada das *trees* de commits usando a *flag* especializada de integração externa:
```bash
git pull origin main --allow-unrelated-histories
```

**Problema 2 (Gargalo Físico do GitHub):** Arquivos excedendo o *hard limit* de 100MB devido a Cubemaps de 8K (*Real Stars Skybox* registrando 192MB) travando o repositório inteiro.  
**Solução 2:** Foi necessária uma limpeza profunda. Excluímos as pastas dos cubemaps irrelevantes, purgamos os *commits* que indexavam metadados gigantes desfazendo o histórico instável (`git update-ref -d HEAD`), permitindo um *upload* otimizado.

---

## 7. INSTRUÇÕES DE EXECUÇÃO 

1. **Clone o Repositório Localmente:**
   ```bash
   git clone https://github.com/ThiLinhares/metaverso-atv01
   ```
   *(O projeto implementa rigorosamente o arquivo `.gitignore` focado na engine Unity, isolando e enviando unicamente diretórios vitais: `Assets`, `Packages` e `ProjectSettings`)*

2. **Abertura e Configuração Unity:**
   - Abra o **Unity Hub** (certifique-se de que está utilizando o **Unity 6**).
   - Acione a opção `Add` e selecione a pasta recém-clonada. O Hub processará o *Registry* e reimportará a URP.

3. **Testando a Navegação na Cena:**
   - Navegue até `Assets/Scenes/SampleScene` e abra a cena com duplo-clique.
   - Acione o botão **Play (▶)** para compilar o ambiente localmente.
   - **Atalhos (PC):**
     - `W, A, S, D` ou Setas Direcionais: Andar fisicamente pelo ambiente.
     - `Mouse (Visão)`: Rotação natural de câmera.
     - `Shift`: Modo de corrida (*Sprint*).
     - `Esc`: Destravar/recuperar o cursor da janela do Editor.
