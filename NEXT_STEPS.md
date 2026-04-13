# Siguientes pasos — nemo

Hola Coni. Tu agente está listo en `/Users/constanza/Documents/Claude/Agents/nemo`.

## Ir al workspace

```bash
cd /Users/constanza/Documents/Claude/Agents/nemo
```


## Subir la rama al fork

```bash
git push -u origin mac-mini-de-constanza.local-nemo-1/live
```

Tu fork vive en: https://github.com/Constanza-Arriagada-Marnell/nemo-mac-mini-de-constanza.local

Para replicar este agente en otro host:

```bash
git clone https://github.com/Constanza-Arriagada-Marnell/nemo-mac-mini-de-constanza.local.git ~/Claude/Agents/nemo
cd ~/Claude/Agents/nemo
git checkout mac-mini-de-constanza.local-nemo-1/live
# luego corre ./setup.sh --regenerate en el nuevo host
```


## Iniciar el agente

```bash
claude
```

## Primer prompt (cópialo tal cual en la primera sesión)

```
Primer arranque del agente nemo. Valida en este orden y corrige lo que falte:

1. `ssh -T git@github.com` responde con mi usuario de GitHub.
2. `gh auth status` reporta una cuenta autenticada con scope repo.
3. El MCP de GitHub responde (lista mis repos públicos como sanity check).
4. La rama actual es mac-mini-de-constanza.local-nemo-1/live y el remote origin apunta al fork.

5. Puedes hacer `git push` sin errores de auth.


Si alguno falla, guíame paso a paso para arreglarlo antes de seguir.
```


## GitHub MCP (no configurado)

El MCP de GitHub no quedó habilitado. Para activarlo:

1. Crea un PAT en https://github.com/settings/tokens con scope `repo`.
2. Añádelo a `.env`:
   ```
   GITHUB_PAT=tu_token_aqui
   ```
3. Edita `agent.yml` y pon `mcps.github.enabled: true`.
4. Corre `./setup.sh --regenerate` para actualizar `.mcp.json`.



## Telegram (chat bidireccional con el agente)

No configuraste Telegram en el wizard. Si quieres chatear con el agente desde tu teléfono:

1. Abre Telegram y habla con [@BotFather](https://t.me/BotFather).
2. Envía `/newbot`, nombre y username (debe terminar en `bot`).
3. Copia el token que te da BotFather.
4. Instala el plugin de chat (una vez por usuario):
   ```bash
   claude plugin install telegram@claude-plugins-official
   ```
5. Dentro de la sesión de Claude, corre `/telegram:configure` y pega el token.
6. Habla con [@userinfobot](https://t.me/userinfobot) para obtener tu `chat_id` numérico.
7. Corre `/telegram:access` en Claude y añade tu `chat_id` a la allowlist.
8. Envía un mensaje al bot y confirma que llega a la sesión.




## Verificar el servicio

```bash
systemctl --user status nemo.service
systemctl --user restart nemo.service   # si necesitas reiniciar
```


## Comandos útiles

```bash
./setup.sh --regenerate          # después de editar agent.yml
./setup.sh --sync-template       # traer mejoras del template al fork
./setup.sh --uninstall           # desmontar el agente
```

---

Cualquier problema, cuéntamelo en la primera sesión y lo diagnosticamos juntos.
