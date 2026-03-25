# 🐣 Rifa de Páscoa

Aplicação web para gestão de uma rifa temática de Páscoa, acessível a qualquer pessoa através do browser, sem necessidade de instalação.

**🔗 Acesso directo:** [tantunescisco.github.io/rifa-pascoa](https://tantunescisco.github.io/rifa-pascoa/)

---

## Como funciona

### Para os participantes

1. **Abre o link** da rifa no browser (computador, telemóvel ou tablet).
2. **Escolhe um número** de 1 a 100 clicando num dos ovos coloridos.
3. **Introduz o teu nome** na janela que aparece e clica em **Confirmar**.
4. O número fica verde com o teu nome e é reservado para ti imediatamente.

> Podes comprar quantos números quiseres. Cada número custa **1 €**.

---

### Prémios

| Lugar | Prémio |
|-------|--------|
| 🥇 1.º | 👕 T-Shirt Personalizada |
| 🥈 2.º | 🛍️ Tote Bag |
| 🥉 3.º | 🕯️ Kit Vela + Gesso Perfumado |
| 4.º | 🎀 Porta-Chaves Laço |

---

### Legenda das cores

| Cor | Significado |
|-----|-------------|
| 🔵🟣🟡🟢🩷 (colorido) | Número disponível — clica para reservar |
| 🟡⏳ (amarelo pulsante) | Número a ser reservado por outra pessoa neste momento |
| 🔴 (vermelho) | Número já vendido |

---

### Funcionamento em tempo real

A aplicação utiliza o **Firebase Realtime Database** para sincronizar o estado entre todos os utilizadores em simultâneo:

- Quando alguém abre o modal para reservar um número, esse número fica **bloqueado** para todos os outros em tempo real.
- Quando a compra é confirmada, o número passa a **vendido** instantaneamente em todos os ecrãs.
- Se alguém fechar o browser ou cancelar sem confirmar, o bloqueio é libertado automaticamente ao fim de **30 segundos**.
- Os dados são guardados permanentemente na base de dados — não se perdem ao fechar o browser.

---

## Modo Admin (correcção de números)

Permite corrigir o nome de um comprador ou libertar um número já vendido.

### Como activar

1. Clica no botão **🔒 Admin** no canto inferior direito do ecrã.
2. Introduz a palavra-passe de administrador.
3. O botão passa a **🔓 Admin ON** — o modo está activo.

### Corrigir um nome

Com o modo admin activo, clica em qualquer número **vermelho** (vendido):
- Edita o nome no campo e clica **✔ Guardar** para actualizar.
- Clica **🗑️ Libertar número** para cancelar a venda e disponibilizar o número novamente.

### Desactivar

Clica novamente no botão **🔓 Admin ON** para sair do modo admin.

> As alterações são sincronizadas em tempo real para todos os utilizadores.

---

```
rifa-pascoa/
└── index.html      # Aplicação completa (HTML + CSS + JavaScript numa só página)
```

---

## Tecnologias utilizadas

- **HTML / CSS / JavaScript** — interface e lógica da aplicação
- **Firebase Realtime Database** — base de dados em tempo real para sincronização entre utilizadores
- **GitHub Pages** — alojamento gratuito da aplicação

---

## Configuração (apenas para administradores)

A aplicação está configurada com o projecto Firebase `rifa-pascoa`. Caso seja necessário reconfigurar:

1. Acede a [console.firebase.google.com](https://console.firebase.google.com)
2. Abre o projecto **rifa-pascoa**
3. Vai a **Build → Realtime Database** e verifica que está activo
4. Em **Definições do projecto → As tuas apps**, copia o objecto `firebaseConfig`
5. Substitui os valores no bloco `FIREBASE_CONFIG` no início do script em `index.html`
6. Faz commit e push:
   ```bash
   git add index.html
   git commit -m "chore: actualizar Firebase config"
   git push
   ```

### Regras de segurança recomendadas (Firebase)

Após o período da rifa terminar, altera as regras da base de dados para **somente leitura**:

```json
{
  "rules": {
    ".read": true,
    ".write": false
  }
}
```

---

## Licença

Projecto de uso pessoal e privado.
