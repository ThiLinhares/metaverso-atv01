# Projeto Final: Meu Primeiro Ambiente VR 🏕️⚒️

[![Unity Version](https://img.shields.io/badge/Unity-6-black.svg)](https://unity.com/)
[![Target](https://img.shields.io/badge/Target-Meta%20Quest%20(Android)-1c1e21.svg)]()
[![Status](https://img.shields.io/badge/Status-Concluído-success.svg)]()

## 📖 Descrição Geral
Este projeto foi desenvolvido como submissão para o **Projeto Final: Meu Primeiro Ambiente VR** do programa **Residência em TIC 29**. O objetivo principal é demonstrar a compreensão dos fundamentos de XR (Extended Reality) através da criação de um ambiente virtual imersivo e navegável.

O cenário construído é um **Acampamento de Ferreiro** com estética *Low Poly*, fortemente inspirado na direção de arte de MMORPGs clássicos (como Ragnarok Online). O ambiente foi projetado com foco em otimização de performance, organização estrutural e garantia de qualidade espacial.

## 🎯 Requisitos Atendidos
O projeto cumpre integralmente os critérios técnicos e de design estabelecidos:

### 1. Configuração Técnica
- **Motor Gráfico:** Unity 6 configurado com versão compatível com Meta SDK.
- **Plataforma Alvo:** Build Settings preparados para plataforma Android (Meta Quest).
- **Integração VR:** Meta XR Core SDK e OpenXR instalados e configurados adequadamente no XR Plugin Management.
- **Acessibilidade:** Implementação de *First Person Controller*, garantindo que a movimentação inicial seja toda feita no PC, sem necessitar de funcionar apenas com o óculos de VR.

### 2. Ambiente Virtual
- Composição com mais de 5 objetos 3D na cena (tenda, fogueira, bigorna, mesa, barris, etc.).
- Plano de chão texturizado (grama) e terreno delimitado onde o usuário pode "caminhar".
- *Skybox* configurado, proporcionando a atmosfera e iluminação corretas ao ambiente ao redor.
- Elementos dispostos coerentemente para formar um ecossistema reconhecível de acampamento.

### 3. Organização e Qualidade 
- **Arquitetura Limpa:** Projeto versionado contendo apenas os diretórios estritamente necessários (`Assets`, `ProjectSettings`, `Packages`).
- **Hierarquia Lógica:** Objetos da cena (`SampleScene`) organizados em pastas lógicas (`Terreno_e_Agua`, `Vegetacao_e_rochas`, `Props_Acampamento`, `Barreiras_Invisiveis`).
- **Padronização:** Nomenclatura clara e consistente de todos os elementos e *GameObjects*.
- **Prevenção de Bugs (Colisão):** Testes de colisão rigorosos aplicados. O mapa possui um sistema de contenção (Paredes Invisíveis e densidade de vegetação) para evitar a queda do jogador (Out of Bounds).

---

## 🎮 Controles de Movimentação (PC)
Para testar o projeto diretamente no Unity Editor pelo computador:
- **`W, A, S, D`**: Movimentar o personagem.
- **`Mouse`**: Controlar a câmera / Visão ao redor.
- **`Esc`**: Liberar o cursor do mouse.

---

## 🧠 Reflexão sobre o Aprendizado
A construção deste ambiente foi uma excelente oportunidade para aplicar fundamentos práticos de Level Design e configuração de ambientes XR. Os principais aprendizados incluíram:
1. **Pipeline de Configuração VR:** O fluxo de preparação do Unity para o Meta Quest, resolvendo dependências entre o Meta XR SDK e o OpenXR.
2. **Otimização de Cena:** A escolha consciente por assets *Low Poly* para garantir alta taxa de quadros (FPS), um critério vital para evitar *motion sickness* em Realidade Virtual.
3. **Ilusão de Escala:** A utilização de barreiras físicas disfarçadas por elementos orgânicos (floresta densa) para guiar a exploração do jogador sem quebrar a imersão.

---

## 👨‍💻 Autor
**Thiago Linhares**
*Desenvolvedor e Analista de Qualidade*
